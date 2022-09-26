# Jungle Templating Box

An easy Web challenge !

Hello Welcome to My write up about this box that i've been played on BDsec CTF 2022 .

> First of all , let's take a view about the web page !!

![image info](https://github.com/Shakun8/BDSecCTF-2022/blob/main/images/view.JPG)
And now let's take a look at the source code that they give us :
```python
from flask import *
app = Flask(__name__)

@app.route('/',methods=['GET', 'POST'])
def base():
    person = ""
    if request.method == 'POST':
      if request.form['name']:
        person = request.form['name']
    palte = '''
    return render_template_string(palte)
if __name__=="__main__":
	app.run("0.0.0.0",port=5000,debug=False)
```
```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Secure Search</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0-beta1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-0evHe/X+R7YkIZDRvuzKMRqM+OrBnVFBL6DOitfPri4tjfHxaWutUpFmBp4vmVor" crossorigin="anonymous">
  </head>
  <body>
    <h1 class="container my-3">Hi, %s</h1>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0-beta1/dist/js/bootstrap.bundle.min.js" integrity="sha384-pprn3073KE6tl6bjs2QrFaJGz5/SUsLqktiwsUTF55Jfv3qYSDhgCecCxMW52nD2" crossorigin="anonymous"></script>
    <div class="container my-3">
        <form action="/" method="post">
            <div class="mb-3">
              <label for="text" class="form-label">Type your name here:- </label>
              <input type="text" class="form-control" name="name" id="text" value="">
            </div>
            <button type="submit" class="btn btn-primary">See magic</button>
          </form>
    </div>
</body>
</html>'''% person
```

From here we can understand that the web page is working with Flask which is a lib on python that can configure backend of the webpage and display it as well .

Cool , now let's HACK xD .

Let's write something in the paramater of name.

![image info](https://github.com/Shakun8/BDSecCTF-2022/blob/main/images/2.JPG)

> as u can see whatever we write is printed out , it's like a variable that we can get the input and we print it .
> since we have this , what comes to my mind is SSTI exploit , we can put some payload to exec some commands and stuff. 
> let's go for it .!!


First i Tested this payload to see if it can be work : `{{7*7}}`


And COOL , as we can see it worked , now let's intercept this request to burpsuite

>Well since the payload is worked and it worked with jinja2 , let's get some payload to read file and exec commands
You can find all this payloads here : https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Server%20Side%20Template%20Injection/README.md

And now let's use this paylaod : `
```python
{{ self._TemplateReference__context.cycler.__init__.__globals__.os.popen('id').read() }}
```

> Let's encode it with url encode and paste it in the name paramater :

![image info](https://github.com/Shakun8/BDSecCTF-2022/blob/main/images/burp.png)

damn , `id` command is executed , now let's see what's files are in this directory with `ls -la`

![image info](https://github.com/Shakun8/BDSecCTF-2022/blob/main/images/burp2.JPG)

> as we can see , we have flag file , let's read it with `cat flag`
> ![image info](https://github.com/Shakun8/BDSecCTF-2022/blob/main/images/burp3.JPG)

Cool , flag : `BDSEC{Y3Y_7H1515_7H3_F146}`

# I Hope you enjoy it !!





