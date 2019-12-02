# Develop_Homework
Description of code for homework "Develop"


This will be organized by location in the file directory starting from the top.

    /Develop/
        /package.json - This file serves as a platform to allow further installation and implementaion of npm modules. It also starts nodemon
        
        /server.js - Sets up the express app and ports that will be used to handle requests, as well as requiring authentication through the passport npm. It also sets up the routes that will be used (/routes/api-routes.js and /html-routes.js). Starting on line 26 it links the ./models folder to sync up with the files on the sequelize database and displays a message to the user.

        /config/
            /config.json - Stores user login info.

            /passport.js - Sets up rules for the passport npm establishing how the user logs into the site and what happens if they enter incorrect information. By comparing what was entered vs what was saved in the "db" at ../models. Then it exports those rules to passport to be used in user authentication.

            /middleware/
                /isAuthenticated.js - Restricts the users actions if not logged in. If user is valid, it proceeds with the request, if not it redirects them to the login/homepage.
        
        /models/
            /index.js - Sets up new sequelize database at /../config/config.json to handle user login info. Then filters through files in the directory, imports the info and stores it under the model variable, and associates it with the db which it then exports to be used in user authentication.

            /user.js - Creates the User model that stores the info when a new account is created and ensures that it is unique and valid, it then hashes their password using bcrypt to enhance security and creates a method to check if that hashed password can be compared with the user entered password. It exports this user model to our sequelize db.
        
        /public/
            /login.html - Sets up the layout of the page users will enter their login info at. Requires js/login.js to run and stylesheets/style.css for styling.

            /members.html - Sets up the layout of the page users will be directed to upon successful login. Requires js/members.js to run and stylesheets/style.css for styling

            /signup.html - Sets up the layout of the page users will create their accounts at. Requires js/signup.js to run and stylesheets/style.css for styling

            /js/
                /login.js - Contains the js functions that define the utility of the forms and buttons on the user login page. It determines what happens when the forms are submitted by doing a post to the api/login route, which if successful redirects to the members page.

                /members.js - This file just does a GET request to figure out which user is logged in and updates the HTML on the page.

                /signup.js - Contains the js functions that define the utility of the forms and buttons on the user signup page. It determines what happens when the forms are submitted by doing a post to the signup route, which if successful redirects to the members page or throws an error.

            /stylesheets/
                /style.css - Contains styling for html files. Looks like all it does is add a 50px margin to the top of the forms on the signup and login pages.

        /routes/
            api-routes.js - Handles the routes for user login, sign up, and log out. Dependant on ../models and ../config/passport for handling user authentication and account info storage.

            html-routes.js - checks if a user is logged in and redirects them to either the members or sign up pages. Dependant on ..config/middleware.isAuthenticated to verify whether or not the user is logged in.


