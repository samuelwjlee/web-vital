# performance-ruler

Measure page loading speed using `performance.mark` and `performance.measure`.

👇🏼 Custom hook defined to dynamically "hook" markers and measure func

```javascript
function usePerformanceMarker(name: string) {
  const start = `${name}-start`
  const end = `${name}-end`

  return {
    startMarker: () => performance.mark(start),
    endMarker: () => performance.mark(end),
    measure: () => performance.measure(name, start, end),
  }
}
```

👇🏼 Consume usePerformanceMarker like this

```javascript
function App() {
  const { startMarker } = usePerformanceMarker('page-load')

  function navigate() {
    startMarker()
  }

  return <button onClick={navigate} />
}

function Page() {
  const { endMarker, measure } = usePerformanceMarker('page-load')

  endMarker()
  measure()

  return <div>hello world</div>
}
```

👇🏼 this is would could be sent to analytics if desired

```json
{
  "name": "page-load",
  "entryType": "measure",
  "startTime": 171.69999998807907,
  "duration": 1006.6999999880791
}
```

![demo](./src/demo.gif)
