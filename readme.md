# React cheat sheet

## Table of contents
* [Custom Hooks](#custom-hooks)
    * [UseFetch](#usefetch)
    * [UseLocalStorage](#uselocalstorage)
* [To Read](#to-read)

### Hooks

#### UseState
```jsx
const [state, setState] = useState(initialStateValue)
```
* initialStateValue can be string, number, object, etc.
* setState is a function to set value for `state`

You can initialize state from a function

```jsx
const [token] = useState(() => {
    const token = window.localStorage.getItem('my-token')
    return token || 'default-token'
})
```

### Custom Hooks

#### UseFetch
```jsx
import { useEffect, useState } from "react"

export const useFetch = url => {
    const [data, setData] = useState()
    const [error, setError] = useState()
    const [loading, setLoading] = useState(false)

    useEffect(() => {
        setLoading(true)
        fetch(url)
            .then(response => response.json())
            .then(setData)
            .catch(setError)
            .finally(() => setLoading(false))
    }, [url])

    return { data, error, loading }
}
```

#### UseLocalStorage

Note: This won't work for SSR

```jsx
import { useEffect, useState } from "react"

const useLocalStorage = (defaultVal, key) => {
  const [value, setValue] = useState(() => {
    const localValue = window.localStorage.getItem(key)
    return localValue ? JSON.stringify(localValue) : defaultVal
  })

  useEffect(() => {
    window.localStorage.setItem(key, JSON.stringify(value))
  }, [value])

  return [value, setValue]
};

export default useLocalStorage
```
### To Read
* [Clean Architecture on Frontend](https://dev.to/bespoyasov/clean-architecture-on-frontend-4311)
