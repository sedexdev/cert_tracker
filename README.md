# 📘 Cert Tracker

[![Lint and Test](https://github.com/sedexdev/cert_tracker/actions/workflows/test.yml/badge.svg)](https://github.com/sedexdev/cert_tracker/actions/workflows/test.yml)

Cert Tracker let's you track all aspects of your next IT certification study progression. I've found that having study resources scattered around on various platforms:

- YouTube
- Reddit
- Udemy
- Medium
- DevTo etc.

leads to either text documents full of links, or annoying spreadsheets, or collections of OneNote notebooks.

Wouldn't it be nice to have all your cert specific resources all in one place?

- Courses
- Video content
- Articles
- Documentation

That's what this app is for!

## ✨ Features

- ✅ Self-hosted Docker container environment with local PostgreSQL data storage
- ✅ Upload course links
- ✅ Course section tracking
- ✅ Upload video/article/documentation resource links in well organised sections
- ✅ Customise images for your resources
- ✅ Import resources into other cert instances
- ✅ Switch between light and dark mode

New features under development include:

- 📌 Configurable email reminders running up to exam day
- 📌 Plotly Dash graphical analysis dashboard to see your progress
- 📌 Cost analysis to see your cert spending
- 📌 In-app WYSIWYG text editor and file tree for managing notes
- 📌 An area for storing links to your practice exams
- 📌 Digital flash cards

## 📦 Installation

### Prerequisites

- A system account with sudo / administrator privileges
- `Git` - https://github.com/git-guides/install-git
- `Docker` - https://docs.docker.com/engine/install/
- `Docker Compose` - https://docs.docker.com/compose/install/
- `wsl2` - https://learn.microsoft.com/en-us/windows/wsl/install (Windows only when using Docker Desktop)

### Get the code

```bash
# Clone the repository
git clone https://github.com/sedexdev/cert_tracker.git
cd cert_tracker
```

## ⚙️ Configuration

Update the 2 .txt files under `cert_tracker/secrets` for the PostgreSQL database password and the Flask app secret:

- `cert_tracker/secrets/postgres-pw.txt`
- `cert_tracker/secrets/secret.txt`

**NOTE**: You should follow best practice and _make these secrets complex_, and avoid exposing them in public places.

## 🛠️ Usage

Run the following commands in the project root - `cert_tracker/`

### Running app containers

- `sudo docker compose up -d` - Mac/Linux
- `docker compose up -d` - Windows (from admin prompt)

In your browser navigate to http://127.0.0.1:8181 to view the application once built.

### Stopping app containers

- `sudo docker compose stop` - Mac/Linux
- `docker compose stop` - Windows (from admin prompt)

### Teardown

If you want to destroy the local images run:

- `sudo docker compose down --rmi local` - Mac/Linux
- `docker compose down --rmi local` - Windows (from admin prompt)

If you also want to destroy the PostgreSQL database run:

- `sudo docker compose down --rmi local -v` - Mac/Linux
- `docker compose down --rmi local -v` - Windows (from admin prompt)

### Open Graph Protocol

Where possible the application will query the URL used to create a `resource` and try to pull Open Graph data from the URL using the Python package `opengraph_py3`. When a site has metadata available through the protocol, form fields will auto-populate with images and other available information.

## 📂 Project Structure

```
cert_tracker/
│
├── .github/              # GitHub workflows and issue templates
├── email/                # Email reminders working directory
├── secrets/              # Local secret
├── src/                  # Source
├── tests/                # Unit and integration tests
├── .gitignore            # Git ignore
├── .pylintrc             # Pylint configuration
├── LICENSE               # MIT license
├── README.md             # This README.md file
└── docker-compose.yml    # Local container orchestration config
```

## 🧪 Running Tests

Create a `.env` file in the root of the project and add the following variables:

```bash
FLASK_ENV=development
FLASK_APP=src
FLASK_DEBUG=True
SECRET_KEY="YOUR_SECRET_KEY"
DATABASE_URL="sqlite:///cert-tracker-db"
API_VERSION="1"
TESTING=True
```

Create a new environment and install the dependencies

```bash
# use your preferred virtual environment - I'm using virtualenv
virtualenv venv
source venv/bin/activate
pip3 install -r src/requirements.txt
```

Run the Flask dev server on `127.0.0.1:5000`

```bash
# with venv active
flask run
```

Run the test suite

```bash
# with venv active
pytest -s tests/
```

## 🙌 Contributing

Contributions are welcome! Please follow the [contributing guidelines](https://github.com/sedexdev/cert_tracker/blob/main/CONTRIBUTING.md) and check for open [issues](https://github.com/sedexdev/cert_tracker/issues).

## 🐛 Reporting Issues

Found a bug or need a feature? Open an issue [here](https://github.com/sedexdev/cert_tracker/issues).

## 🧑‍💻 Authors

- **Andrew Macmillan** – [@sedexdev](https://github.com/sedexdev)

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/sedexdev/cert_tracker/blob/main/LICENSE) file for details.

## 📋 Change log

- 08/01/2025 - Uploaded v1.1.0 - Image file uploads [5db06a0](https://github.com/sedexdev/cert_tracker/commit/396b4aa80e8df66e1919d6c81675f06155db06a0)
- 17/12/2024 - BUG FIX - MODULE_NOT_FOUND error during `npm` setup in `Dockerfile` [d657a0c](https://github.com/sedexdev/cert_tracker/commit/d657a0ce10e4e38b8623ef92b95b3df77a1ba2da)
- 13/12/2024 - Uploaded v1.0.0
