# Pre-Tutorial Setup
1. Clone this directory and run npm install to install the node modules. 
2. Cd into the react-context tutorial folder and run npm start. You should see a list with a button that doesn't function at the moment.

# useContext tutorial

## The old way of passing state through prop drilling (Wring way!)

1. create a state isDay
2. Add Onclick to the button
3. pass that state to the List and then to the List item to use (this is prop drilling WRONG!)

4. delete those states being passed.


## Making use of useContext
for this example we are creating a button that changes the color properties of certain elements

1. Create Context Folder with ThemeContext.js as a component
 - import createContext & useState.
 - create & export const ThemeContext = createContext()
 ```export const ThemeContext = createContext(); ```
 - create the component ThemeContextProvider that returns <ThemeContext.Provider> ... </ThemeContext.Provider>
    ``` return (
    <ThemeContext.Provider>
    </ThemeContext.Provider> 
    ```
- Create 3 states:
    - state isDay --> boolean. This is the general state that toggles onClick
    - state light --> object with css properties
    - state dark --> object with css properties
        
- Create a handleClick function (that sets isday to the opposite) that is also passed as a value to the button and fired when clicked.
``` 
    const handleClick = () => {
      setIsDay( !isDay );
  }
 ```
- Pass the states in as props with value = 
```<ThemeContext.Provider value={{isDay, light, dark, handleClick:handleClick}}> ```
- Remember to nest the {children} inside of <ThemeContext>.


2. On App.js
- Import ThemeContextProvider to index.js (main import)
- Wrap the entire returned components inside <ThemeContextProvider>

3. Wherever you want to use those state values.
- import useContext and the ThemeContext  
- create a new const theme that changes depending on the state of isDay
- desctructure the values into a useContext(ThemeContext)
    ```
    const {isDay, light, dark} = useContext(ThemeContext);
    const theme = isDay ? light : dark;
    ```
- add the new style tag to the item you would like to change on click of the button. E.g:
```
 <div className="App" style = {{background:theme.bg, color:theme.color }}>
```

