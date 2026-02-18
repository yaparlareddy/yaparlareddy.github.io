# Personal Page & Todo List

This repository contains:
1.  **Personal Page**: A portfolio website located in the `docs/` folder.
2.  **Todo List App**: A Python-based todo application located in the `todo/` folder.

## How to Host the Personal Page on GitHub

1.  **Create a Repository**: Go to GitHub and create a new repository (e.g., `my-personal-page`).
2.  **Push Code**:
    ```bash
    git add .
    git commit -m "Initial commit with personal page and todo app"
    git branch -M main
    git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
    git push -u origin main
    ```
3.  **Enable GitHub Pages**:
    *   Go to your repository **Settings**.
    *   Scroll down to the **Pages** section (or click "Pages" in the left sidebar).
    *   Under **Source**, select `Deploy from a branch`.
    *   Under **Branch**, select `main` and then select the `/docs` folder (this is important!).
    *   Click **Save**.

Your site will be live at `https://YOUR_USERNAME.github.io/YOUR_REPO_NAME/`.

## Todo List App

The todo list application is in the `todo/` directory.
To run it:
```bash
cd todo
python main.py
```
