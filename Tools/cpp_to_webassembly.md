https://mbebenita.github.io/WasmExplorer/
obtengo file.wasm


luego

```js
<script>
  WebAssembly.instantiateStreaming(
    fetch('file.wasm')
  )
  .then(obj => {
    use the result
  })

</script>
```
