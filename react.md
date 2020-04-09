## Notes de cours sur React JS


### Les contextes

[Demo Live](https://codepen.io/guhur/pen/dyogxyK)


L'objectif de partager des données à une partie de l'application. 
Lorsque ces données changent, les composants qui se sont inscrits à ces données sont mis à jour. 

On définit un contexte avec : 
```jsx
const myContext = React.createContext(valeur_par_defaut);
```

ensuite, on définit un `Provider` qui réagit au changement d'une donnée:

```jsx
<myContext.Provider value={my_data}>
     { 
// ici on place les composants qui ont besoin d'accéder à my_data
   }
 </myContext.Provider>
```

Le `Provider` doit donc être rechargé à chaque fois que `my_data` à changer.

En utilisant des classes, le rechargement s'opère grâce à la fonction `setState` en plaçant le `Provider` dans une classe composant React :

```jsx
class MyProvider extends React.Component {
  state = {
     counter: 0,
     increment: () => this.setState({counter: this.state.counter + 1})
  }
  render() {
    return(
            <myContext.Provider value={this.state}>
                {this.props.children}
            </myContext.Provider>
        )
  } 
}
```

De l'autre côté, pour qu'un enfant puisse accéder à `my_data`, on injecte `my_data` dans un HOC (higher order component) :

```jsx
const Button = (props) => <button onClick={props.increment}>Incrémenter le compteur ({props.counter})
</button>;
const withCounter = Component => {
    const NewComponent = props => {
        return(
            <myContext.Consumer>
                { value => <Component {... value} {... props}/>}
            </myContext.Consumer>
        )
    }
    return NewComponent
}
const ButtonWithCounter = withCounter(Button);
```

Ainsi, si un enfant appelle la fonction `increment` , il appelle le `setState` de `MyProvider`, qui appelle `render`, lequel re-génère cet enfant. Il suffit donc de placer ButtonWithCounter comme un enfant de MyProvider: 

```jsx
const App = () => <MyProvider><ButtonWithCounter /></MyProvider>;
```

Le HOC est une fonction compliquée, mais il suffit de retenir qu'il ajoute un attribut (une `props`) qui contient `my_data`.

Si on récapitule le fonctionnement :

1. Lorsqu'on clique sur le bouton, on fait appel à `props.increment`.
2. `props.increment` a été injecté dans le composant grâce au HOC `withCounter`.
3. Il s'agit en fait la valeur donnée par `this.state.increment` définit dans `MyProvider`.
4. `this.state.increment` fait appel à `this.setState`.
5. `this.setState` fait ensuite appel à `render`.
6. `render` reconstruit `ButtonWithCounter`
7. `ButtonWithCounter` affiche la nouvelle valeur du compteur


### Utilisation des contextes en React avec l'API Hooks

Plutôt que d'utiliser les classes, React vous propose d'utilise des fonctions, lesquelles sont nettement moins longues à écrire -- et donc sont plus simples à maintenir.
La différence entre les deux est illustrée [ici](https://codepen.io/guhur/pen/RwPeXZO): 

```jsx
const Button1 = (props) => {
  const { onClick, children } = props; 
  return (<button onClick={onClick}>{children}</button>);
}
  
class Button2 extends React.Component {
  render() {
    const {children, onClick} = this.props;
    // équivalent à :
    // const onClick = props.onClick;
    // const children = props.children
    return(
      <button onClick={onClick}> 
        { children }
      </button>
    );
  }
} 
```

De la même manière qu'avec les [classes](./context_react.md), on définit un contexte et un Provider :

```jsx
const counterContext = React.createContext({counter: 0});

class CounterProvider extends React.Component {
  state = {
     counter: 0,
     increment: () => this.setState({counter: this.state.counter + 1})
  }
  render() {
    return(
            <counterContext.Provider value={this.state}>
                {this.props.children}
            </counterContext.Provider>
        )
  } 
}
```

#### Remplacer le HOC par `useContext`

Le provider partage des données à l'ensemble de l'application. Mais comment peut-on souscrire à ces données ?
Plutôt que de définir un HOC, nous allons utiliser la fonction `useContext` pour consommer les données partagées par un contexte :

```jsx
const useCounter = () => {
  const {counter, increment} = useContext(counterContext);
  return {counter, increment};
};
```

Pour utiliser le compteur :
```jsx
const Button = (props) => {
  const {counter, increment} = useCounter();
  return (<button onClick={increment}>Incrémenter ({counter})</button>);
}
```

La demo est disponible sur [codepen](https://codepen.io/guhur/pen/ZEGmzam).

Que se passe-t-il étape par étape ?

1. Lorsqu'on clique sur le bouton, on fait appel à `increment`.
2. `increment` a été injecté dans le composant grâce à `useCounter`.
3. `useCounter` est juste une ré-écriture des données stockées dans le `counterContext`
4. `increment` est donc toujours la fonction `this.state.increment` définit dans `CounterProvider`.
5. De même qu'avec les classes, `this.state.increment` fait appel à `this.setState`, qui fait ensuite appel à `render`.
6. `render` reconstruit `Button`
7. `Button` affiche la nouvelle valeur du compteur.


#### Ré-écrire le `Provider` avec `useState`

On peut également remplacer la méthode `this.setState` du Provider avec la nouvelle Hooks API de React : 

```jsx
const CounterProvider = (props) => {
  // 0 est la valeur par défaut du compteur
  // setCounter est équivalent à l'ancienne méthode `this.setState` :
  
  const [counter, setCounter] = useState(0);
  const increment = () => setCounter(counter + 1);
  
  return(
    <counterContext.Provider value={{counter, increment}}>
      {props.children}
    </counterContext.Provider>
  )
}
```

La demo est disponible sur [codepen](https://codepen.io/guhur/pen/gOpQYKW).


