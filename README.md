# Jenkins Docker Hub Pipeline

A minimal Flask application packaged with Docker and built and pushed to Docker Hub by Jenkins.

## Project structure

```text
jenkins-dockerhub-pipeline/
├── app/
│   ├── __init__.py
│   └── app.py
├── tests/
│   └── test_app.py
├── Dockerfile
├── requirements.txt
├── Jenkinsfile
└── README.md
```

## Run locally

Install the requirements and start the application:

```sh
python -m pip install -r requirements.txt
python -m app.app
```

Open <http://localhost:5000>.

## Run tests

```sh
python -m unittest discover -s tests
```

## Configure Jenkins

1. Make sure the Jenkins agent has Python and Docker installed and can access the Docker daemon.
2. Add a Jenkins **Username with password** credential for Docker Hub with the ID `dockerhub-credentials`.
3. In `Jenkinsfile`, replace `your-dockerhub-username` in `DOCKERHUB_REPO` with your Docker Hub username.
4. Create a Jenkins Pipeline job that uses this repository's `Jenkinsfile`, then run the job.

The pipeline runs the tests, builds versioned and `latest` image tags, then pushes both to Docker Hub.
