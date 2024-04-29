# codehelium 👾

Codehelium is a lightweight IDE for the web that compiles and executes your code using Pyodide/Emscripten/Webassembly.

Currently, **only Python code editing is supported** using our React component.

## Installation 🖥️

To get started with using codehelium in your React application run `npm i codehelium`, import the component and you're good to go!
```jsx
import PythonEditor from 'codehelium'
...
<PythonEditor width="90vw" height="80vh" />
```
## More Examples 😎

### Obtaining Console Outputs from Parent Components
Oftentimes, you may desire to obtain the stdout or stderr from user-written code in codehelium IDE components. For a given state variable in your parent component, you can pass the corresponding setter function via the `consoleOutputSetter` prop to utilise console outputs from user-written code in the PythonEditor component.
```jsx
import PythonEditor from 'codehelium';
import { useEffect, useState } from 'react';

function App() {
    const [consoleOutputs, setConsoleOutputs] = useState([]);

    useEffect(() => {
        console.log("Printing from App... Console output received");
        console.log(consoleOutputs);
    }, [consoleOutputs])

    return (
        <div>
            <PythonEditor width="90vw" height="80vh" 
            consoleOutputSetter={setConsoleOutputs} />
        </div>
    );
}

export default App;
```
### Using an External Pyodide Instance
If you have initialised Pyodide elsewhere in your application, you can pass this instance to the `PythonEditor` component by using the `pyodideInstance` prop. The following example demonstrates how to do so:
```jsx
import PythonEditor from 'codehelium';
import { loadPyodide } from 'pyodide';
import { useEffect, useState } from 'react';

function App() {
    const [myPyodideInstance, setMyPyodideInstance] = useState(null);

    useEffect(() => {
        async function createPyodideInstance() {
            let pyodide = await loadPyodide({
            indexURL: window.location.href + "/pyodide"
            });
            
            setMyPyodideInstance(pyodide);
        }

        // Initialize pyodide instance in parent component
        createPyodideInstance();
    }, []);

    return (
        <div>
            <div className="w-screen h-screen grid place-content-center">
                <PythonEditor width="90vw" height="80vh"
                pyodideInstance={myPyodideInstance}/>
            </div>
        </div>
    );
}

export default App;
```
This is especially useful for those developing applications that use a singleton model for Pyodide functionality.
## Guide to Contributing 🫶
To get started with contributing, fork this repository and then run the following once you have cloned the forked repo:
```
npm install
npm start
```
Library components can then be changed by visiting `src/lib/`, with changes reflected in the development server (from running `npm start`). Once complete, send a PR (filled with basic details) to bring your changes into this repo!

## Support this Project 💛
Starring this repo and sending PRs with useful features/improvements are always appreciated and welcomed!
