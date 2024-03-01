### Heroku Deployment of Pet Pals Application

#### Overview
This guide outlines the process for deploying the Pet Pals application to Heroku. Pet Pals is an application that captures the name, latitude, and longitude of a pet to plot its location on a map. The focus here is on the deployment steps which can be applied to deploy your own applications to Heroku.

#### Prerequisites
- A Heroku account. Sign up at [Heroku](https://www.heroku.com).

### Deployment Steps

#### Part 1: Create a New Repository
1. **Setup**: Clone the [Pet Pals app](./Starter) starter files into a new GitHub repository named **Pet_Pals**.

#### Part 2: Configuration Files
2. **Environment Setup**: Create a new conda environment with Python 3.7 (excluding Anaconda) and activate it:
   ```sh
   conda create -n pet_pals_env python=3.7
   conda activate pet_pals_env
   ```
   If issues arise, use `source activate pet_pals_env` instead.
   
3. **Dependencies**:
   - Install `gunicorn` for running Flask apps in production: `pip install gunicorn`.
   - Install `psycopg2` or `psycopg2-binary` for PostgreSQL database support: `pip install psycopg2-binary`.
   - Install Flask, Flask-SQLAlchemy, and pandas: 
     ```sh
     pip install flask flask-sqlalchemy pandas
     ```
   - Initialize the database with `python initdb.py`.
   - Make the `run.sh` file executable: `chmod a+x run.sh`.
   - Test the app locally using `./run.sh` and navigate to `127.0.0.1:5000`.

4. **Prepare for Heroku**:
   - Generate `requirements.txt` with `pip freeze > requirements.txt`. Ensure to downgrade SQLAlchemy to `1.3.23` to avoid compatibility issues.
   - Create a `Procfile` and add `web: gunicorn pet_pals.app:app` to instruct Heroku on running the app.

#### Part 3: Creating the Heroku App
5. **Heroku Setup**: Log into Heroku, create a new app with a unique name, and connect your GitHub repository for deployment.
   
6. **Deploy**: Manually deploy your branch through the Heroku dashboard.

#### Part 4: Preparing the Database
7. **Database Setup**: Add Heroku Postgres from the **Resources** section. Use the free plan and provision it.
   
8. **Database Configuration**: Obtain the database credentials from the **Settings** tab and use them in your application.
   
9. **Initialize Database**: Use the Heroku CLI to run `initdb.py` with your app's name to set up the database schema.

10. **Launch**: Your app should now be live. Use `heroku open -a <name of your app>` to view it.

#### Final Notes
- Ensure longitude values are negative for correct plotting on the US map.
- The deployment process primarily involves setting up the application environment, preparing configuration files, deploying through Heroku, and initializing the database. Follow these steps carefully to ensure a smooth deployment.

This README provides a step-by-step guide for deploying applications to Heroku, demonstrated with the Pet Pals application. Adjust the instructions as necessary for your specific project requirements.