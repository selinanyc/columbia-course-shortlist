# Columbia course shortlist

An agent skill that helps find and shortlist [Columbia University](https://www.columbia.edu/) courses to take or audit. It uses the public [Directory of Classes](https://doc.sis.columbia.edu/) and [CULPA](https://culpa.info/) reviews, includes [Vergil](https://vergil.columbia.edu/) deep links, and drafts audit-request emails for you to review and send.

## How to use

Drop `SKILL.md` into a Cursor or other agent skills folder, for example:

```text
.cursor/skills/columbia-course-shortlist/SKILL.md
```

Or paste the file into any agent that supports `SKILL.md` skills. Then ask for a term, subjects, and whether you want to enroll or audit.

## Limitations

- Vergil is behind Cloudflare, so days and times have to be read in a browser. The skill does not try to bypass that.
- The Directory of Classes no longer shows meeting times.
- A new term may not be published yet (the listing returns 404).
- CULPA coverage is thin for professional schools; many courses have no reviews.

## Disclaimer

Unofficial. Not affiliated with Columbia University. This skill never logs in with a UNI and never registers or enrolls anyone. Public endpoints may change.

---

# 哥伦比亚大学选课短名单

一个 agent skill，用来查找并筛选哥伦比亚大学可以选修或旁听的课程。它使用公开的课程目录（Directory of Classes）和 CULPA 评课，附上 Vergil 深链接，并起草旁听申请邮件，由你自己审阅后发送。

## 用法

把 `SKILL.md` 放到 Cursor 或其他 agent 的 skills 目录，例如：

```text
.cursor/skills/columbia-course-shortlist/SKILL.md
```

也可以把文件内容粘贴到任何支持 `SKILL.md` 的 agent。然后说明学期、院系，以及你是选课还是旁听。

## 限制

- Vergil 有 Cloudflare 保护，上课日和时间需要用浏览器查看。本 skill 不会尝试绕过它。
- 课程目录已不再显示上课时间。
- 新学期的课表可能尚未发布（页面返回 404）。
- 专业学院在 CULPA 上的评课很少，很多课没有评价。

## 声明

非官方，与哥伦比亚大学无关。本 skill 从不用 UNI 登录，也不会替任何人注册或选课。公开接口可能会变化。
