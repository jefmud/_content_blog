Here is an example of simple form handling with Minimus.

Today we are going to create a very simple form with minimus.  First let's create a minimal Minumus app.

<pre>
from minimus import Minimus, parse_formvars

app = Minimus(__name__)

@app.route('/hello')
def hello(environ):
    return "Hello for Minimus!"

app.run()
</pre>
 

This should get us up and running.

Let's check it out by using our browser to go to http://localhost:5000/hello this will yield the message Hello from Minimus!

Let's change the program up a little bit.  We're going to add a form to the program.  This form will have a name and a message, similar to a guestbook.  We are going to create a simple form in the program using three quotes to do a multiline string.

<pre>
from minimus import Minimus, parse_formvars

app = Minimus(__name__)

simple_form = """
<h1>My Form</h1>
<form method="post">
  Name<br />
  <input name="name" type="text"><br />
  Enter your message<br />
  <textarea name="message"></textarea><br />
  <input type="submit">
</form>
"""

@app.route('/formdemo', methods=['GET','POST'])
def hello(environ):
    if environ['REQUEST_METHOD'] == 'POST': #check the type of request
        fields = parse_formvars(environ) #parse the fields returned from the environment
        return f"<h1>Hello</h1><p>Thanks for for the message:\n {fields}.</p>"
    return simple_form

app.run()
</pre>
 

That's all there is to pick up the form fields!  One thing that you will note is that fields is/are returned as a Multidict type.  This is a common Python extra type that allows a dictionary to have multiple keys with the same name.

Why would you want to do this?  Mostly because it allows you to have a response where a key is defined "temporally".  You could have an initial answer followed by additional specifications later on.  Or you could possibly have a search that allows for multiple search terms.  The possibilities are endless.

What should be noted is that if you access fields as a dictionary, you will get the FIRST field with that name and the rest will be ignored.

meta#author#Evan R. Muday

meta#created_at#May 28, 2022

meta#title#Minimus Example 2

meta#subtitle#you can even handle forms!

meta#image_url#https://images.unsplash.com/photo-1653671637237-befb4bcfe142

meta#is_published#true

meta#slug#minimus-example-2
