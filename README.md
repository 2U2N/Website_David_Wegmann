# David Wegmann Academic Website

This repository contains a minimal Quarto website for David Wegmann, intended as a clean academic and professional identity hub.

The site is designed to be low-maintenance:

- Quarto renders the website.
- GitHub Actions deploys the rendered site to GitHub Pages.
- Publications are generated from a Zotero/Better BibLaTeX export.
- The CV is generated locally as a PDF and embedded on the website.

## Repository Structure

Editable website files:

- `index.qmd` for the home page
- `projects.qmd` for project descriptions
- `publications.qmd` for the generated publications page
- `cv.qmd` for the embedded PDF CV page
- `cv-source.qmd` for the editable CV PDF source
- `contact.qmd` for affiliation and contact details
- `styles.css` for visual styling
- `_quarto.yml` for site configuration and navigation

Generated or data files:

- `My_Publications.bib` for publications exported from Zotero
- `files/cv.pdf` for the public CV PDF shown on the CV page
- `_site/` for the rendered website output

Public assets:

- `images/` for public website images
- `files/` for public downloadable files

## Update Publications From Zotero

The website Publications page and the Publications section of the generated CV PDF both draw from `My_Publications.bib`.

The intended workflow is to maintain a Zotero collection called **My Publications** and export that collection automatically using Better BibTeX / Better BibLaTeX.

One-time Zotero setup:

1. Install the Better BibTeX plugin for Zotero.
2. In Zotero, create or maintain a collection named **My Publications**.
3. Put only public publications and public preprints/outputs in that collection.
4. Right-click the **My Publications** collection.
5. Choose **Export Collection...**.
6. Choose **Better BibLaTeX** as the export format.
7. Enable **Keep updated**.
8. Save the export in this repository root as `My_Publications.bib`.

After Zotero updates `My_Publications.bib`:

```sh
quarto render
```

Important privacy check before publishing:

```sh
rg -n "file =|/Users/|Zotero/storage" My_Publications.bib
```

If that command finds anything, remove private local fields before publishing. Local Zotero file paths should not be committed to a public website repository. In Better BibTeX settings, consider omitting fields such as `file` from exports.

`publications.qmd` uses `nocite: '@*'`, which means every BibTeX entry in `My_Publications.bib` appears automatically, even when it is not cited manually.

## Update The CV PDF

The website CV page, `cv.qmd`, embeds `files/cv.pdf`. The editable CV source is `cv-source.qmd`.

`cv-source.qmd` also uses `My_Publications.bib`, so publication changes require regenerating the CV PDF if the embedded CV should show the latest publication list.

Use this workflow whenever the CV text or publications change:

```sh
quarto render cv-source.qmd --to typst --output cv.pdf
mv cv.pdf files/cv.pdf
quarto render
```

Commit both `cv-source.qmd` and `files/cv.pdf` when publishing CV updates. GitHub Actions deploys the committed PDF; it does not regenerate the CV PDF automatically.

Only include CV information that is meant to be public.

## Edit Common Site Content

Home page:

- Edit `index.qmd`.
- The profile photo is stored in `images/` and referenced from `index.qmd`.
- If replacing the image, update the image path in `index.qmd`.

Projects:

- Edit `projects.qmd`.
- Keep project descriptions short and public-facing.

Contact:

- Edit `contact.qmd`.
- Use institutional/public contact details only.

Navigation and site metadata:

- Edit `_quarto.yml`.
- The active pages are Home, Projects, Publications, CV, and Contact.
- Update `site-url` after the GitHub repository URL is known.

Styling:

- Edit `styles.css`.
- Keep the design minimal and readable.

## Render Locally

Install Quarto, then render the website:

```sh
quarto render
```

The rendered site is written to `_site/`.

## Preview Locally

Run:

```sh
quarto preview
```

Quarto will start a local preview server and print the preview URL.

## Deploy With GitHub Pages

The workflow in `.github/workflows/publish.yml` renders the Quarto website and deploys `_site/` to GitHub Pages.

Manual GitHub setup:

1. Initialize Git locally if needed: `git init`
2. Create a GitHub repository.
3. Push this repository to GitHub.
4. In the GitHub repository, go to **Settings > Pages**.
5. Set **Source** to **GitHub Actions**.
6. Push to the `main` branch and confirm the workflow succeeds.

## Add A Custom Domain Later

This site is not configured for a custom domain yet. To add one later:

1. Configure the domain in **Settings > Pages** on GitHub.
2. Add the required DNS records with the domain provider.
3. Add a `CNAME` file only after the domain is ready.
4. Update `site-url` in `_quarto.yml`.

## Maintenance Checklist

Before publishing or pushing changes:

- Run `quarto render`.
- If publications changed, regenerate `files/cv.pdf`.
- Check `My_Publications.bib` for private local paths.
- Verify institutional contact information.
- Include only public publications, reports, CV information, images, and downloadable files.
- Do not include raw data, participant data, private reports, unpublished drafts, credentials, API keys, or restricted institutional files.
- Confirm the GitHub Pages workflow publishes from `_site/`.
