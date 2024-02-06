import os
import requests
from datetime import datetime

# Configuration
REPO_NAME = 'leenhassan/Endocrine_blog'  # Replace with your GitHub username and repository name
BRANCH = 'main'  # or 'gh-pages' if you use a custom branch for GitHub Pages
PATH = '_posts/Blog.md'  # Path within your repository where blog posts are stored
TOKEN = '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'  # Your GitHub Personal Access Token
EDITOR = 'code'  # Your preferred editor command (e.g., 'code' for VS Code, 'subl' for Sublime Text)

POST_TEMPLATE = """---
layout: post
title:  "{}"
date:   {}
categories: blog
tags: [sample, markdown]
author: Leen Hassan
summary: "This Blog talks about the endocrine system"
---

Your content goes here.
"""

def create_new_post(title):
    filename_date = datetime.now().strftime('%Y-%m-%d')
    formatted_date = datetime.now().strftime('%Y-%m-%d %H:%M:%S +0000')
    filename = f"{filename_date}-{title.lower().replace(' ', '-')}.md"
    content = POST_TEMPLATE.format(title, formatted_date)
    return filename, content

def push_to_github(filename, content):
    url = f'https://api.github.com/repos/{REPO_NAME}/contents/{PATH}{filename}'
    data = {
        "message": f"Add new post: {filename}",
        "branch": BRANCH,
        "content": content.encode('utf-8').hex()
    }
    headers = {
        "Authorization": f"token {TOKEN}",
        "Accept": "application/vnd.github.v3+json"
    }
    response = requests.put(url, json=data, headers=headers)
    return response.json()

def main():
    title = input("Enter the title of your blog post: ")
    filename, content = create_new_post(title)
    response = push_to_github(filename, content)
    if response.get('content'):
        print(f"Blog post created successfully: {response['content']['html_url']}")
    else:
        print("Failed to create blog post:", response)

if __name__ == "__main__":
    main()
