---
title: How to delete a git folder
date: 2021-11-14 12:08:54
featuredImage: /post-images/2021-11-14-how-to-delete-a-git-folder.webp
draft: false
tags:
  - Git
---

```bash
rm -rf .git
```

Let's examine the code we wrote to get a little bit better understanding.

**rm** stands for remove, pretty straightforward.

**-r** flag means recursively to target all files, and **-f** means force to pass through all warnings.

(This flag ensures the command will be executed properly)

**.git** the invisible file we want to target.

---

### Why deleting a git folder?

Well, use cases can be different, but basically, it is a convenient command for resetting git history, so you can then run

```bash
git init
```

And reinitialize the repo.

### Alternative

Git folder is by default invisible on Windows, so you can make it visible via this setting.

Step one: find folder options in the windows start menu:

![](/post-images/2021-11-image-1.webp)Step two:

![](/post-images/2021-11-image-2.webp)Here we are!

![](/post-images/2021-11-image-3.webp)
