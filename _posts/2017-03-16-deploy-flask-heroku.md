---
layout: post
title: "Deploy flask app to heroku"
date:   2017-3-16 0:06:32
tags: heroku flask
categories: "Flask"
---
# 0. Login
```
heroku login
```
# 1. Create app
```
heroku create [app-name]
```

# 2. Add remote 
```
heroku git:remote -a [app-name]
```

# 3. runtime.txt
Specifiy the python version you'd like to use
```
python-3.6.0
```

# 4. Procfile
A text file in the root directory of your application, to explicitly declare what command should be executed to start your app
```
web: python [main.py]
```

# 5. requirement.txt
save current to requirement.txt
```
pip freeze > requirement.txt
```

# 6. main
Get $PORT from environment argument
```
if __name__ == "__main__":
	port = int(os.environ.get("PORT", 5000))
	app.run(host='0.0.0.0',port=port);
```

# 7. Deploy to the heroku master
```
git add [files]
git commit -m '[comments]'
git push heroku master
```

# 8. Scale the app
```
heroku ps:scale web=1
```

# 9. Open app
```
heroku open
```


