You can find out anyone's github email if it's set publicly in git by hitting this url for any given user and searching for "email".

  https://api.github.com/users/xxxxxxx/events/public

Gives back:

    "author": {
                "email": "vicki.boykis@gmail.com",
                "name": "Vicki Boykis"
              }

There is potentially [a way to wipe it](https://help.github.com/articles/changing-author-info/) from old commits. 
