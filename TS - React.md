<style>
.block {
    background-color: #f5f5f5;
    padding: 6px 10px;
    border-radius: 5px;
    box-shadow: 0 0 5px 0px grey;margin:15px 0px;
    padding-bottom: 1px;
    font-size:13px;
    transition: all 1s ease;
    overflow: hidden;
}
code {
    font-size: 12px;
}
.block2 {
    background-color: #fffae7;
    padding: 6px 10px;
    border-radius: 5px;
    box-shadow: 0 0 5px 0px grey;margin:15px 0px;
    padding-bottom: 1px;
    font-size:13px;
    color: #7c1212;
    font-weight: 600
}

.detail .long {
    display: none;
  }

  .detail:hover .short {
    display: none;
  }
  .detail:hover .long {
    display: inline;
  }

  .detail .short {
    background-color: #FFF6E9;
  }
</style>

### Some examples
The file extensions changed from .js/.jsx to .ts/.tsx

```js
type HeadingProps = { title: string }

const Heading = ({ title }: HeadingProps) => {
    return ();
}

export default Heading;
```

```js
type SectionProps = {
    title?: string,
    children: ReactNode
}

export const Section = ({ children, title = "Subheading" }: SectionProps) => {
    return (
        <section>
            <h2>{title}</h2>
            <p>{children}</p>
        </section>
    )
}
```

```js
import Heading from './components/Heading'
import { Section } from './components/Section'

function App() {
    return (
        <>
            <Heading title={"Hello"}>
            <Section title={"Something else"}>
                <h1>Section children</h1>
            </Section>
        </>
    )
}

export default App
```

```js
import { useState } from 'react'

const Counter = () => {
    const [count, setCount] = useState(1) // could be inferred
    const [count, setCount] = useState<number>(1)
    const [count, setCount] = useState<number | null>(null) // if no initial value

    return (
        <>
            <h1>Count is {count}</h1>
            <button onClick={() => setCount(prev => prev + 1)}>+</button>
            <button onClick={() => setCount(prev => prev - 1)}>-</button>
        </>
    )
}

export default Counter
```

A variation of the previous two snippets.
```js
// App.tsx
function App() {
    const [count, setCount] = useState<number>(1)

    return (
        <>
            <Heading title={"Hello"}/>
            <Counter>
                <h1>Count is {count}</h1>
            </Counter>
        </>
    );
}

// Counter.tsx
import { ReactNode } from 'react';

type CounterProps = {
    setCount: React.Dispatch<React.SetStateAction<number>>,
    children: ReactNode, 
}

const Counter = ({ setCount, children }: CounterProps) => {
    return (
        <>
            {children}
            <button onClick={() => setCount(prev => prev + 1)}>+</button>
            <button onClick={() => setCount(prev => prev - 1)}>-</button>
        </>
    )
}

export default Counter
```

List example
```js
import { ReactNode } from 'react'

interface ListProps<T> {
    items: T[],
    render: (item: T) => ReactNode
}

const List = <T>({ items, render }: ListProps<T>) => { // don't recognize <T> as a generics this way
const List = <T extends {}>({ items, render }: ListProps<T>) => { // one way
const List = <T,>({ items, render }: ListProps<T>) => { // other way
    return (
        <ul>
            {items.map((item, i) => (
                <li key={i}>
                    {render(item)}
                </li>
            ))}
        </ul>
    )
}

export default List;

// other component
<List items={["A", "B"]} render={(item: string) => <span>{item}</span>}/>
```





### React hooks

```js
import { useEffect } from 'react'

function App() {

    useEffect(() => {
        console.log('mount')

        return () => console.log('unmount')
    }, [])

    return (

    )
}

export default App
```


// TODO useCallback