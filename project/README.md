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
                return redirect(url_for('login'))
        else:
            return redirect(url_for('login'))

    return render_template("login.html")
```
The code above is the login system. To directly connect the login system when the user operates it, the route is "/". There is a login button that request.method change to POST which allows the user to send data when the button is pressed. Uname and psw are gotten value from the user input by using request.form.get method is used to access form data sent in a POST request where the name of the input is defined as "username" and "password". Create a hash to find user who has the same username as the user's input and make it run. Since the user should exist if the input is correct, use the if statement to pick only the cases where the user exists. If the user exist, next check the accuracy of the password by using check_hash() which returns True or force from the input of saved hash and input hash. If it is True, receive return the redirect method, which is used to redirect the user to a different endpoint in Flask. This is used to navigate the user to another page or URL, "main" which is main page. If the result of check_hash is False, return redirect to the url for "login" again. Also, if the request.method is not "GET", while the user doesn't press the login button, the return is render_template, which is used to render HTML templates and return them as a response to the client. The render_template function allows you to use template files, written in HTML "login.html".








## Session
```.py
from flask import session
app = Flask(__name__)
app.secret_key = 'your_secret_key'

# login()
session["current_user"] = uname

# see_comment_anime()
comment = f"""INSERT into animes_comment(comment, date, anime_id, username, likes)
                   VALUES ('{input_comment}','{datetime.now()}',{anime_id},'{session["current_user"]}' ,0)"""
        print(comment)
```
In Flask, sessions are used to persist data across requests from the same client. The session object allows to store information specific to a user from one request to another. For example, session["curren_user"] is defined as uname in the login function. Even though the function is different, the value is available, as you can see in see_comment_anime function. In this function, session["current_user"] is used as the username of who uses the website at that time when a query called comment is created. The Session allows for the application to recognize the value defined in a function in a different function.

## Edit comment
```.py
@app.route('comment/<int:food_id>/edit/<int:comment_id>', methods=['GET', 'POST'])
def edit_comment(food_id,comment_id):
    my_db = DatabaseBridge('project.db')
    if request.method == 'POST':
        comment = request.form.get('edited_comment')
        my_db.run_query(f"UPDATE foods_comment SET comment='{comment}',date='{datetime.now()}' WHERE id={comment_id}")
        my_db.close()
        return redirect(url_for('see_comment_foods', food_id=food_id))
    return redirect(url_for('see_comment_foods', food_id=food_id))

# see_comment_foods()
comment_info = my_db.search(query=f"""SELECT * from foods_comment where food_id = {food_id} """, multiple=True)
```

```.html
# food_comment.html
{% if session["current_user"] == r[4] %}
  {% for r in comment_info %}
    <form method="POST" action="{{ url_for('edit_comment', food_id=r[3], comment_id=r[0]) }}">
    <button type="submit">Edit</button>
  {% endfor %}
{% endif %}
```

The code above shows how comments can be edited. The function gets information by using HTML.The commen_inofo is defined in see_comment_foods() which returns render_template(food_comment_html).
Comment_info selects all the information saved in foods_comment including, id, comment, date, food_id, username, and likes which food_id matches r[3], and comment_id=r[0]. The method is only available when r[4], the username that represents the writer of the comment is the same as session["current_user"], which means the user logged in at that time. Thus only the comment the user wrote can be edited by the user.

Connecting database called "project.db" by using DatabaseBridge. When a user presses the Edit button, request.method changes to "POST". Edited comments can be gotten by request.form.get which input name is "edited_comment". The comment is replaced by run_query which has a query to update the comment and date when the query is inserted. The database is closed after it. and redirect to the URL "see_comment_foods" which requires input food_id and returns render_template to food_comment.


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


