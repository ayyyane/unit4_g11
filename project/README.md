# Unit4 Raddit
<img width="1000" alt="Screenshot 2024-05-21 at 10 31 43" src="https://github.com/ayyyane/unit4_g11/assets/142702159/774e568a-2a88-4cc0-b589-7bce96273467">


# Criteria C Development
## the technique used
- Python inside HTML
- CSS designs
- For loops 
- If statements
- Token-based authentication
- Lists and Dictionaries
- HTTP server
- POST, GET Requests
- SQLite databases
- Hash
- Flask
  
## Login system 
```.py
@app.route('/',methods=['GET','POST'])
def login():
    if request.method == 'POST': # means the form was submitted
        uname = request.form.get('username')
        psw = request.form.get('password')
        q_hash = f"""SELECT hash FROM users where name = '{uname}'"""
        results_hash = my_db.search(query=q_hash, multiple=False)
        if results_hash:
            if check_hash(results_hash[0],psw) == True
                return redirect(url_for('main'))
            else:
                flash("the password is wrong","error")
                return redirect(url_for('login'))
        else:
            flash("The user doesn't exist", "error")
            return redirect(url_for('login'))

    return render_template("login.html")
```
The code above is the login system. To directly connect the login system when the user operates it, the route is "/". There is a login button that request.method change to POST which allows the user to send data when the button is pressed. Uname and psw are gotten value from the user input by using request.form.get method is used to access form data sent in a POST request where the name of the input is defined as "username" and "password". Create a hash to find user who has the same username as the user's input and make it run. Since the user should exist if the input is correct, use the if statement to pick only the cases where the user exists. If the user exist, next check the accuracy of the password by using check_hash() which returns True or force from the input of saved hash and input hash. If it is True, receive return the redirect method, which is used to redirect the user to a different endpoint in Flask. This is used to navigate the user to another page or URL, "main" which is main page. If the result of check_hash is False, return redirect to the url for "login" again. Also, if the request.method is not "GET", while the user doesn't press the login button, the return is render_template, which is used to render HTML templates and return them as a response to the client. The render_template function allows you to use template files, written in HTML "login.html".




## Session
```.py
from flask import session
app = Flask(__name__)
db_name = "project.db"
my_db = DatabaseBridge(db_name)
app.secret_key = 'your_secret_key'



```
For the 

## likes 

## follow

# Criteria D Functionality
4 min video on the functionality of the code

https://drive.google.com/file/d/1YxEGyczQcM2PgU9xevph7fZCfHdTd1ia/view?usp=drive_link


# Criteria E Evaluation+
## Evaluation table
Client
| Criteria                                             | Met or not | Feedback                                                                 |
|------------------------------------------------------|------------|--------------------------------------------------------------------------|
| A login/registration system                          | Met        | It is better to add see password button which is hidden.                 |
| A posting system to EDIT/CREATE/DELETE comments.     | Met        | Good                                                                     |
| A system to add/remove likes                         | Met        | It is better to create a button to work both likes and remove likes. |
| A system to follow/unfollow users, topics, or groups. | Met        | Good                                                                     |
| A profile page with relevant information             | Met        | Good                                                                     |

Another client
| Criteria                                             | Met or not | Feedback                                             |
|------------------------------------------------------|------------|------------------------------------------------------|
| A login/registration system                          | Met        | It is unuseful that I couldn't see the password I typed. |
| A posting system to EDIT/CREATE/DELETE comments.     | Met        | Great                                                |
| A system to add/remove likes                         | Met        | I love it as I can add likes as much as I push the button. I pushed likes 100 times for One Piece!!|
| A system to follow/unfollow users, topics, or groups. | Met        | It is more convenient to follow from the comment page. |
| A profile page with relevant information             | Met        | It is better for the user to choose a profile picture. |



## Extensibility
1. Add a show password button that allows users to switch between visible/invisible passwords to protect user information safety and improve convenience.
2. Add options for the user to choose a profile picture.
3. Limit the number of likes/unlikes or make a button to switch between likes and remove likes when the user presses the button. However, a client felt inconvenienced by the current button systems, while another client likes one which allows users to add likes as many as they want. Thus more considerations are needed.

## Appendix


**fig** Contact between developer and client for evaluation of website

![IMG_7F48EAB4EFB7-1](https://github.com/ayyyane/unit4_g11/assets/142702159/20298cbb-4404-4776-bda2-4e41ff57aef7)

**fig** Contact between developer and client for evaluation of website


