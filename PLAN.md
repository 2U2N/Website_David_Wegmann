# Quarto Academic Website Plan

## Summary

- Create a clean, low-maintenance personal academic website for David Wegmann.
- Use Quarto as the source format and GitHub Pages as the hosting target.
- Keep public website content in editable `.qmd` files.
- Use placeholder text where real information is missing.
- Do not commit or push changes unless explicitly requested.

## Files To Create

- `_quarto.yml`
- `index.qmd`
- `projects.qmd`
- `publications.qmd`
- `cv.qmd`
- `cv-source.qmd`
- `contact.qmd`
- `styles.css`
- `README.md`
- `.gitignore`
- `.github/workflows/publish.yml`
- `images/.gitkeep`
- `files/cv.pdf`

## Site Structure

- Home
- Projects
- Publications
- CV page with embedded public PDF generated from `cv-source.qmd`
- Contact

The home page will quickly communicate who David Wegmann is, what he studies, and where visitors can find research, publications, projects, CV details, and contact information.

## Deployment Approach

- Render the CV PDF locally from `cv-source.qmd` to `files/cv.pdf`.
- Render the Quarto site to `_site`.
- Use GitHub Actions to install Quarto, render the site, upload `_site` as a GitHub Pages artifact, and deploy it.
- Configure GitHub Pages manually in the repository settings to use GitHub Actions.
- Do not configure a custom domain yet.

## Manual GitHub Steps

1. Initialize Git locally if needed.
2. Create a GitHub repository.
3. Push the local repository to GitHub.
4. In GitHub repository settings, enable Pages and set the source to GitHub Actions.
5. Confirm the first workflow run succeeds.
6. Replace placeholder profile, contact, CV source, publication, talk, and profile-link information before public sharing.

## Quality Checks

- Run `quarto render cv-source.qmd --to typst --output cv.pdf`, then move the generated `cv.pdf` to `files/cv.pdf`.
- Run `quarto render`.
- Confirm all navbar pages render.
- Confirm internal links target existing `.qmd` pages.
- Confirm placeholder links and missing information are clearly marked.
- Keep raw data, private reports, unpublished drafts, participant data, credentials, and institutional files out of the public repository.
