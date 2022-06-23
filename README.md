# Evaluate
<html>
    <head>
      <link rel='stylesheet' type='text/css' media='screen' href='https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css'>
      <link rel="stylesheet" href="https://pyscript.net/alpha/pyscript.css" />
      <script defer src="https://pyscript.net/alpha/pyscript.js"></script>
    </head>

  <body><center><br>

<textarea name="input_text" id="input_text" placeholder="Enter Your Text"></textarea><br><br>

<button id="solve" type="button" class="button is-primary" pys-onClick="evaluate">Evaluate</button>

<button id="clear" type="button" class="button is-danger" pys-onClick="clear">Clear</button><br><br>
    
<p id='output'></p>

<py-script>
  input_text=Element("input_text")

  output=Element("output")

  def clear(*args,**kwargs):
    input_text.clear()
    output.clear()
  
  def evaluate(*args,**kwargs):

    s=input_text.value
    try:
      e=eval(s)
      output.write(e)
    except:
      output.write("Error")

</py-script>
</center></body>
</html>
