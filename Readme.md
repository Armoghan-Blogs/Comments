# 💬 4rm0Byte — Comments

<p align="center">

  <img src="https://raw.githubusercontent.com/Armoghan-Blogs/4rm0Byte/main/.github/assets/banner.png" alt="4rm0Byte Banner" width="800">

</p>

<div align="center">

[![Repository](https://img.shields.io/badge/GitHub-Comments-181717?style=for-the-badge\&logo=github)](https://github.com/Armoghan-Blogs/Comments)
[![Utterances](https://img.shields.io/badge/Comments-Utterances-5865F2?style=for-the-badge\&logo=github)](https://utteranc.es/)
[![GitHub Actions](https://img.shields.io/github/actions/workflow/status/Armoghan-Blogs/Comments/discord-comments.yml?style=for-the-badge\&logo=github-actions\&label=Discord%20Notifications)](https://github.com/Armoghan-Blogs/Comments/actions)
[![Issues](https://img.shields.io/github/issues/Armoghan-Blogs/Comments?style=for-the-badge\&logo=github)](https://github.com/Armoghan-Blogs/Comments/issues)
![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)

</div>

---

## 📖 About

Welcome to the **4rm0Byte Comments** repository.

This repository serves as the dedicated backend for the comment system used by **[4rm0Byte](https://4rm0byte.netlify.app)**. Comments on 4rm0Byte are powered by **[Utterances](https://utteranc.es/)**, an open-source commenting widget that uses GitHub Issues as its backend. Instead of maintaining a separate database or comment server, every article's comments are stored and managed through GitHub Issues in this repository. The repository also contains a **GitHub Actions** workflow that automatically sends new comment notifications to Discord, making it easy to keep track of conversations happening across the blog.

---

## 🏗️ Architecture

The comment system follows a simple and transparent architecture:

```text
┌──────────────────────────┐
│        4rm0Byte          │
│      Hugo Website        │
└────────────┬─────────────┘
             │
             │ Utterances
             ▼
┌──────────────────────────┐
│       GitHub Issues      │
│                          │
│  Armoghan-Blogs/Comments │
└────────────┬─────────────┘
             │
             │ issue_comment
             ▼
┌──────────────────────────┐
│      GitHub Actions      │
│                          │
│ Discord Comment Workflow │
└────────────┬─────────────┘
             │
             │ Discord Webhook
             ▼
┌──────────────────────────┐
│         Discord          │
│     Comment Alerts       │
└──────────────────────────┘
```

### 🔄 Comment Flow

1. A visitor opens an article on **4rm0Byte**.
2. Utterances loads the comment section.
3. The visitor authenticates with GitHub.
4. Utterances creates or uses the GitHub Issue associated with the article.
5. The visitor submits a comment.
6. GitHub creates an `issue_comment` event.
7. GitHub Actions detects the new comment.
8. The workflow collects and formats the comment information.
9. A branded Discord embed is generated.
10. The notification is delivered through the configured Discord webhook.

---

### 🧭 Issue Mapping

4rm0Byte uses:

```text
issueTerm = "pathname"
```

Therefore, an article's URL pathname is used by Utterances to identify its corresponding GitHub Issue.

For example:

```text
4rm0Byte Article
       │
       ▼
/posts/example-article/
       │
       ▼
GitHub Issue
       │
       ▼
Comments for that article
```

This keeps comments associated with their corresponding pages without requiring a separate database.

---

## 🔔 Discord Notifications

New comments are automatically forwarded to Discord through GitHub Actions.

The workflow is located at:

```text
.github/
└── workflows/
    └── discord-comments.yml
```

The workflow listens for:

```yaml
on:
  issue_comment:
    types:
      - created
```

This is important because Utterances stores comments as GitHub Issue comments.

### ✨ Discord Notification

The workflow creates a branded Discord embed containing information such as:

* 💬 Comment content
* 👤 Comment author
* 🖼️ GitHub avatar
* 📄 Associated article / issue
* 🕐 Comment timestamp
* 📏 Comment length
* 🔗 Direct link to the comment
* 🔗 Direct link to the GitHub Issue
* 🧵 Issue number
* 🛡️ Protected Discord mentions

The notification is sent through a Discord webhook stored securely as a GitHub Actions repository secret.

---

## 🔐 Secrets

The Discord webhook **must never be committed to this repository**.

The workflow expects the following repository secret:

```text
DISCORD_WEBHOOK_URL
```

Configure it under:

```text
GitHub
  → Repository Settings
  → Secrets and variables
  → Actions
  → Repository secrets
```

The workflow accesses it using:

```yaml
${{ secrets.DISCORD_WEBHOOK_URL }}
```

### ⚠️ Security

Never place the Discord webhook directly inside:

* Workflow source code
* Hugo templates
* JavaScript
* Markdown files
* Public configuration files
* Commit history

A Discord webhook URL should be treated as a secret.

---

## 🛠️ Technologies

* [x] **GitHub Issues** — Comment storage and discussion backend
* [x] **Utterances** — Website commenting system
* [x] **GitHub Actions** — Comment notification automation
* [x] **Discord Webhooks** — Discord notification delivery
* [x] **Python** — Comment formatting and Discord payload generation
* [x] **Bash / cURL** — Webhook delivery
* [x] **GitHub CLI** — Repository and Issue management

---

## 🤝 Contributing

This repository is infrastructure for the **4rm0Byte** comment system rather than a traditional software project.

Contributions are generally not expected.

However, suggestions and improvements related to:

* Comment reliability
* Discord notifications
* Workflow security
* Accessibility
* Spam prevention
* Automation
* Performance
* Developer experience

are welcome.

For significant changes, please open an Issue first to discuss the proposed improvement.

---

## 📜 License

This project is licensed under the MIT License.

See the [LICENSE](https://github.com/Armoghan-Blogs/Comments/blob/main/LICENSE) file for details.

---

## 🌐 4rm0Byte

This repository powers the commenting infrastructure for: **[4rm0Byte](https://4rm0byte.com)**.

The main website repository is available at: **[github.com/Armoghan-Blogs/4rm0Byte](https://github.com/Armoghan-Blogs/4rm0Byte)**

---

## 📧 Contact

For questions, suggestions, or inquiries:

* 📩 **[armoghanblogs@gmail.com](mailto:armoghanblogs@gmail.com)**
* 💻 **GitHub:** [Armoghan-Blogs](https://github.com/Armoghan-ul-Mohmin)
* 🌐 **Website:** [4rm0Byte](https://4rm0byte.netlify.app)

---

<div align="center">

### 💬 Built for 4rm0Byte

**Powered by GitHub Issues + Utterances + GitHub Actions + Discord**

⭐ If you find the project interesting, consider starring the repositories.

</div>
