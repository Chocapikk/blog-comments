# Blog Comments Repository

This repository hosts GitHub Discussions for comments on [Chocapikk's Cybersecurity Blog](https://chocapikk.com/).

## About

Comments on blog posts are powered by [giscus](https://giscus.app/), which uses GitHub Discussions to store and manage comments. This provides a privacy-friendly, ad-free commenting system.

## How it works

- Each blog post automatically creates or links to a GitHub Discussion
- Visitors can comment using their GitHub account
- All comments are stored in this repository's Discussions section
- No ads, no tracking, fully open source

## 📖 Tutorial: How to Comment on Blog Posts

### For Readers

#### Step 1: Find the Comment Section
- Scroll to the bottom of any blog post on [chocapikk.com](https://chocapikk.com/)
- You'll see a comment section powered by giscus

#### Step 2: Sign in with GitHub
- Click on the comment box
- You'll be prompted to sign in with your GitHub account
- If you don't have a GitHub account, you can [create one for free](https://github.com/signup)

#### Step 3: Write Your Comment
- Type your comment in the text box
- You can use Markdown formatting:
  - **Bold**: `**text**`
  - *Italic*: `*text*`
  - `Code`: `` `code` ``
  - [Links](https://example.com): `[text](url)`
  - Lists, quotes, and more!

#### Step 4: Submit
- Click "Comment" to post your comment
- Your comment will appear immediately and be stored in this repository's Discussions

### Features

- ✅ **Reactions**: React to comments with 👍, ❤️, 😄, 🎉, and more
- ✅ **Reply**: Reply directly to other comments
- ✅ **Edit/Delete**: You can edit or delete your own comments
- ✅ **Notifications**: Get notified when someone replies to your comment
- ✅ **Privacy**: No ads, no tracking, your data stays on GitHub

### Tips

- **Be respectful**: Keep discussions constructive and friendly
- **Use Markdown**: Format your comments for better readability
- **Check notifications**: GitHub will notify you of replies
- **View on GitHub**: Click on any comment to view it directly on GitHub

## For Blog Owners: Setting Up giscus

If you want to set up giscus for your own blog, here's how:

### Prerequisites

1. A GitHub account
2. A public GitHub repository (or one where you can enable Discussions)
3. A static website (Hugo, Jekyll, Next.js, etc.)

### Step-by-Step Setup

#### 1. Create a Repository for Comments
```bash
gh repo create blog-comments --public --description "GitHub Discussions for blog comments"
```

#### 2. Enable GitHub Discussions
- Go to your repository settings
- Scroll to "Features"
- Enable "Discussions"

Or via API:
```bash
gh api repos/OWNER/REPO -X PATCH -f has_discussions=true
```

#### 3. Install the giscus App
- Visit [https://github.com/apps/giscus](https://github.com/apps/giscus)
- Click "Install" or "Configure"
- Select your comments repository
- Authorize the installation

#### 4. Get Your Configuration
- Visit [https://giscus.app/](https://giscus.app/)
- Enter your repository name (e.g., `username/blog-comments`)
- Select your discussion category (usually "General")
- Choose your preferences (theme, language, etc.)
- Copy the generated script

#### 5. Add to Your Blog

**For Hugo:**
1. Create `layouts/partials/comments.html`:
```html
{{- if not .Params.hideComments -}}
  {{- $giscus := .Site.Language.Params.giscus -}}
  {{- if and $giscus $giscus.repo $giscus.repoId -}}
  <hr style="margin-top: 40px; margin-bottom: 40px;" />
  <div style="max-width: 100%;">
    <script src="https://giscus.app/client.js"
      data-repo="{{ $giscus.repo }}"
      data-repo-id="{{ $giscus.repoId }}"
      data-category="{{ $giscus.category }}"
      data-category-id="{{ $giscus.categoryId }}"
      data-mapping="{{ default "pathname" $giscus.mapping }}"
      data-strict="0"
      data-reactions-enabled="{{ default "1" $giscus.reactionsEnabled }}"
      data-emit-metadata="0"
      data-input-position="{{ default "bottom" $giscus.inputPosition }}"
      data-theme="{{ default "preferred_color_scheme" $giscus.theme }}"
      data-lang="{{ default "en" $giscus.lang }}"
      data-loading="lazy"
      crossorigin="anonymous"
      async>
    </script>
  </div>
  {{- end -}}
{{- end -}}
```

2. Include it in your post template (usually `layouts/_default/single.html`):
```html
{{- partial "comments.html" . -}}
```

3. Add configuration to `config.toml`:
```toml
[Languages.en-us.params.giscus]
  repo = "username/blog-comments"
  repoId = "YOUR_REPO_ID"
  category = "General"
  categoryId = "YOUR_CATEGORY_ID"
  mapping = "pathname"
  reactionsEnabled = "1"
  inputPosition = "bottom"
  theme = "preferred_color_scheme"
  lang = "en"
```

**For Other Static Site Generators:**
- Simply add the script tag from giscus.app to your post template
- The script will automatically handle comment creation and management

### Getting Repository and Category IDs

**Repository ID:**
```bash
gh api repos/OWNER/REPO | jq -r '.node_id'
```

**Category IDs:**
```bash
gh api graphql -f query='query { repository(owner: "OWNER", name: "REPO") { discussionCategories(first: 10) { nodes { id name } } } }' | jq -r '.data.repository.discussionCategories.nodes[] | "\(.id) \(.name)"'
```

### Benefits of giscus

- 🚫 **No ads**: Unlike Disqus, giscus is completely ad-free
- 🔒 **Privacy-friendly**: No tracking, your data stays on GitHub
- 🆓 **Free**: Completely free and open source
- 🎨 **Customizable**: Themes, languages, and more
- 🔄 **GitHub integration**: Comments are stored in GitHub Discussions
- 📱 **Responsive**: Works great on mobile devices

## Repository Structure

- **Discussions**: All blog post comments are stored here
- **Categories**: Comments are organized by category (General, Announcements, etc.)

## Links

- Blog: https://chocapikk.com/
- giscus: https://giscus.app/
- GitHub Discussions: [View Discussions](https://github.com/Chocapikk/blog-comments/discussions)
- giscus Documentation: https://github.com/giscus/giscus

## Contributing

This repository is automatically managed by giscus. Comments are created automatically when visitors comment on blog posts. You don't need to interact with this repository directly unless you want to:

- Moderate discussions
- View all comments
- Manage discussion categories
- Export comments

## License

MIT License - See [LICENSE](LICENSE) file for details.

---

*This repository is automatically managed by giscus. Comments are created on-demand when visitors interact with blog posts.*
