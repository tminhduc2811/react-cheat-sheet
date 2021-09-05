# React cheat sheet

## Table of contents
* [Custom Hooks](#custom-hooks)
    * [UseFetch](#usefetch)
    * [UseLocalStorage](#uselocalstorage)

### Custom hooks

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
