# React cheat sheet

## Table of contents
* [Custom Hooks](#custom-hooks)
    * [UseFetch](#usefetch)

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
