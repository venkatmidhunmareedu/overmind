## Overmind
Overmind is a LaTeX-based resume workflow for creating a clean base resume and generating role-specific variants quickly. It is designed for iterative editing in Cursor/VS Code, ATS-oriented tuning, and reproducible PDF output (`resume.pdf`) from source files in this repository.

The recommended workflow is:
- maintain a stable, generic base resume on `master`
- create job-description-specific branches for tailored versions
- keep each branch focused on one target role/company so updates are easy to track and reuse


## Development Guide : 

1. Fork this repository to your own GitHub account (recommended) so you own your resume history and customizations.
2. Clone your fork locally:
	- `git clone https://github.com/<your-username>/overmind.git`
3. Keep your base resume on `master`, then create one branch per job description:
	- `git checkout -b jd-<company>-<role>`
	- Example: `git checkout -b jd-acme-backend-engineer`
4. Install the necessary extensions and packages for your operating system. 
5. Build the project using 
	- Press `Ctrl + shift + p` to open the control panel and search for `LaTex Workshop: Build LaTex Project`
	- Or Simply Press `Ctrl + Shift + B` (which is a preset, see the settings yourself)
6. Go through the `resume.pdf` output and verify content/format. (Build updates the PDF on save, similar to live reload.)

## Quick-Start Templates

Use the templates in `templates/` for faster resume setup.

- Current editable template:
  - `templates/jakes-resume/jakes-resume.tex`
- Quick usage:
  - copy this template into `resume.tex` as your starting point, or
  - reuse selected sections and tune them for your target role
- Note:
  - `.aux`, `.fls`, `.fdb_latexmk`, `.log`, and `.out` files in template folders are generated build artifacts


### Steps to preview the resume in VS Code or any other VS Code Fork. (Followed by the agent skill usage for quick setup and tuning)

1. Find `LaTex Workshop` extension and install it. ([https://marketplace.cursorapi.com/items/?itemName=James-Yu.latex-workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop))
2. If your platform is:
- Linux :
	- `sudo apt install texlive-latex-base texlive-fonts-recommended latexmk`
- Windows:
	- You have install `Perl` from [https://strawberryperl.com/](https://strawberryperl.com/)
	- if it's not installed already, open the `MikTeX` Package Manager and install the `latexmk` package.
- Mac:
	- It’s probably already installed.
	- If not, open `TeX Live Utility`, search for `latexmk` and install it.
	- If you prefer using the Terminal:
		- `sudo tlmgr install latexmk`

## Agent Skill Usage

This repository includes reusable Cursor agent skills in `.cursor/skills/`.

### 1) overmind-setup

Use this when you want the agent to set up or verify local LaTeX tooling for this repo.

- Trigger examples:
  - "Setup this repo"
  - "Install dependencies for resume build"
  - "Make LaTeX build work in Cursor"
- What it does:
  - Checks build prerequisites for your OS
  - Guides/install steps for `LaTeX Workshop` and `latexmk`
  - Helps build and verify `resume.pdf`

### 2) overmind-tune

Use this when you want the agent to tailor your resume to a specific job description for better ATS matching.

- Trigger examples:
  - "Tune my resume for this job description"
  - "Improve ATS score for this role"
  - "Tailor resume keywords to JD"
- What it does:
  - Extracts high-value keywords from the job description
  - Applies Rule of Three for critical skills (Summary, Skills, Experience)
  - Rewrites bullets with measurable impact and ATS-safe phrasing
  - Preserves parser-safe format (standard headers, single-column style, consistent dates)

### How to invoke

- Direct prompt style:
  - "`Use overmind-setup and help me build resume.pdf`"
  - "`Use overmind-tune with this JD and rewrite resume.tex`"
- Slash workflow style:
  - `/create-skill` to add or extend custom skills for your workflow

