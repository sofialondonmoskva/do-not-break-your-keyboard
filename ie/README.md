##### ie8 - console.log

Using console.log in ie8 without developer tools opened will stab you in the back.

```
console.log("must print this!")
// console is undefined - bzzz...bazinga!
```

> [http://stackoverflow.com/questions/3326650/console-is-undefined-error-for-internet-explorer](http://stackoverflow.com/questions/3326650/console-is-undefined-error-for-internet-explorer)

```
<script type="text/javascript"> if (!window.console) console = {log: function() {}}; </script>
```

