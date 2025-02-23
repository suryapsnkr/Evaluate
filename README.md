# Evaluate
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PyScript Evaluator</title>
    <link rel="stylesheet" type="text/css" media="screen" href="https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css">
    <link rel="stylesheet" href="https://pyscript.net/releases/2024.1.1/core.css">
    <script type="module" src="https://pyscript.net/releases/2024.1.1/core.js"></script>
</head>

<body>
    <center><br>
        <textarea id="input_text" placeholder="Enter Your Expression"></textarea><br><br>
        <button id="solve" type="button" class="button is-primary">Evaluate</button>
        <button id="clear" type="button" class="button is-danger">Clear</button><br><br>
        <p id='output'></p>
    </center>

    <script type="py" id="pyscript">
        from js import document
        from pyodide.ffi import create_proxy  # ✅ Fix Pyodide event issue

        def clear(event):
            document.getElementById("input_text").value = ""
            document.getElementById("output").innerText = ""

        def evaluate(event):
            input_text = document.getElementById("input_text").value
            output = document.getElementById("output")

            try:
                result = eval(input_text)  # ⚠️ Be careful using eval (Security risk)
                output.innerText = f"Result: {result}"
            except Exception as e:
                output.innerText = f"Error: {e}"

        # ✅ Fix Pyodide event issues
        evaluate_proxy = create_proxy(evaluate)
        clear_proxy = create_proxy(clear)

        document.getElementById("solve").addEventListener("click", evaluate_proxy)
        document.getElementById("clear").addEventListener("click", clear_proxy)
    </script>
</body>
</html>
