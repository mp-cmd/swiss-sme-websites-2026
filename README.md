---
license: cc-by-4.0
language:
- fr
- en
- de
pretty_name: "Swiss SME Websites 2026 (10,000 sites audited)"
size_categories:
- n<1K
tags:
- switzerland
- sme
- websites
- seo
- structured-data
- llms-txt
- data-protection
- web-measurement
configs:
- config_name: measures_by_canton
  data_files: data/measures_by_canton.csv
- config_name: measures_by_region
  data_files: data/measures_by_region.csv
- config_name: measures_by_legal_form
  data_files: data/measures_by_legal_form.csv
- config_name: measures_switzerland
  data_files: data/measures_switzerland.csv
- config_name: population_by_canton
  data_files: data/population_by_canton.csv
- config_name: population_by_region
  data_files: data/population_by_region.csv
- config_name: population_by_legal_form
  data_files: data/population_by_legal_form.csv
- config_name: platforms_by_group
  data_files: data/platforms_by_group.csv
- config_name: copyright_year_by_canton
  data_files: data/copyright_year_by_canton.csv
---

# Swiss SME Websites 2026: 10,000 sites audited, canton by canton

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23192819.svg)](https://doi.org/10.5281/zenodo.23192819)

Aggregated measurements of 10,000 websites of Swiss small and medium-sized
businesses, drawn at random from the Swiss commercial register in September
2026. Proportions only: no company name, no website address, no figure for a
group of fewer than 30 sites.

- **Study page (FR):** https://hallebardier.com/etude-sites-pme-suisses/
- **Study page (EN):** https://hallebardier.com/en/swiss-sme-website-study/
- **Study page (DE):** https://hallebardier.com/de/studie-websites-kmu-schweiz/
- **Source JSON:** https://hallebardier.com/etude-pme-2026.json
- **DOI (Zenodo, all versions):** https://doi.org/10.5281/zenodo.23192819
- **GitHub:** https://github.com/mp-cmd/swiss-sme-websites-2026
- **Hugging Face:** https://huggingface.co/datasets/mp-cmd/swiss-sme-websites-2026
- **Author:** Hallebardier (Maxime Perriard), Fribourg, Switzerland
- **Licence:** CC BY 4.0

## How to cite

> Hallebardier (2026). *Swiss SME Websites 2026: 10,000 sites audited, canton by canton* [Data set]. Zenodo. https://doi.org/10.5281/zenodo.23192819

When you publish a figure from this dataset, please link to the study page.

## Method in short

1. **Sample.** Swiss commercial register (Zefix, Federal Office of the
   Commercial Register, via LINDAS open data). Legal forms: GmbH/Sàrl, AG/SA,
   sole proprietorships, general partnerships. All 26 cantons. One eighth of the
   register, chosen by the first character of the MD5 hash of the Zefix
   identifier: uniform, proportional to each canton, reproducible. Excluded:
   bankruptcies, liquidations, holding and vehicle companies, listed companies,
   pharmacies, group subsidiaries. 91,834 companies read, 82,059 kept,
   41,841 processed to reach 10,000 proven websites.
2. **Websites.** Domains formed from the company name (no search engine). A
   site counts only with proof that it belongs to the company (name, UID,
   address or town). "With proven site" is therefore a floor, and "no address"
   does not mean "no website".
3. **Audit.** 9,970 sites reachable. Measured: HTTPS, mobile viewport,
   structured data (JSON-LD), meta description, title length, robots.txt,
   sitemap.xml, llms.txt, privacy page, copyright year in the footer, platform,
   HTML reception time from a server in Switzerland.
4. **Access rules.** robots.txt read and respected before any page (RFC 9309),
   crawl-delay honoured up to 60 s, nothing behind a login, no form sent, no
   security test. Robot name: `HallebardierEtude`.

## Margins of error (95 %)

| Scope | Margin |
|---|---|
| Population (41,841 companies) | ±0.5 point |
| National measures (9,970 sites) | ±1 point |
| German-speaking Switzerland | ±1.2 points |
| Romandie | ±2.1 points |
| Ticino | ±4.7 points |
| Canton | about 1.96 × √(0.25 / n) × 100, with n = `sites` |

## Files

| File | Rows | Content |
|---|---|---|
| `data/measures_switzerland.csv` | 1 | All measures, national |
| `data/measures_by_canton.csv` | 26 | All measures per canton |
| `data/measures_by_region.csv` | 3 | Per language region |
| `data/measures_by_legal_form.csv` | 4 | Per legal form |
| `data/population_by_canton.csv` | 26 | Share of companies with a proven site, uncertain, no address |
| `data/population_by_region.csv` | 3 | Same, per region |
| `data/population_by_legal_form.csv` | 4 | Same, per legal form |
| `data/platforms_by_group.csv` | long | Platform shares (only the 12 platforms with 50+ sites nationally) |
| `data/copyright_year_by_canton.csv` | long | Number of sites per footer year (years before 2016 grouped into 2016) |
| `data/etude-pme-2026.json` | | The original JSON, with French keys and definitions |

## Column definitions

All `_pct` columns are percentages of reachable sites in the group, unless the
name says otherwise.

| Column | Definition |
|---|---|
| `sites` | Reachable sites audited in the group |
| `https_pct` | Final URL served over HTTPS |
| `mobile_viewport_pct` | Page declares a mobile viewport |
| `html_reception_median_s` | Median time to receive the home page HTML (not full rendering) |
| `html_over_2_5s_pct`, `html_over_5s_pct` | HTML received in more than 2.5 s / 5 s |
| `html_median_kb` | Median HTML size of the home page |
| `structured_data_jsonld_pct` | At least one JSON-LD block |
| `meta_description_pct` | A meta description is present |
| `title_12_chars_plus_pct` | Title of 12 characters or more |
| `sitemap_xml_pct`, `robots_txt_pct`, `llms_txt_pct` | File present. A file served as HTML counts as absent. A server refusal (403, timeout) is left out of the denominator, given in the matching `_base` column |
| `privacy_page_found_pct` | A page or PDF whose link or address contains "confidentialité", "protection des données", "Datenschutz" or "privacy", with at least 800 characters of text. A legal notice or Impressum page is not counted. Base in `privacy_page_base` |
| `wordpress_pct` | Platform detected as WordPress |
| `wordpress_version_readable_count` | WordPress sites whose version could be read |
| `wordpress_outdated_pct_of_readable` | Share of those not on a current version |
| `copyright_year_shown_pct` | A © year appears on the home page |
| `copyright_2y_plus_old_pct_of_shown`, `copyright_5y_plus_old_pct_of_shown` | Share of shown years that are 2+ / 5+ years old |
| `with_proven_site_pct` | Population: a site answers at an address formed on the company name and carries proof it is theirs |
| `uncertain_pct` | Population: a domain answers without proof, or DNS did not answer, or robots.txt refused reading |
| `no_address_pct` | Population: every address formed on the name is free, for sale or under construction |
| `robots_refusal_pct` | Population: share left out because robots.txt refused the study robot |

## Limits

- Speed is the reception of the HTML code, not what a visitor sees.
- Platforms are counted, never judged.
- A privacy statement inside a legal notice page without its own name is not
  counted as a privacy page.
- Per-site data is not published and will be deleted by 27 March 2027.

---

# Sites des PME suisses 2026 : 10 000 sites audités, canton par canton

Mesures agrégées de 10 000 sites de PME suisses, tirées au hasard du registre
du commerce en septembre 2026. Proportions seulement : aucun nom d'entreprise,
aucune adresse de site, aucun chiffre sur un groupe de moins de trente sites.

**Citer :** Hallebardier (2026). *10 000 sites de PME suisses, canton par
canton.* https://hallebardier.com/etude-sites-pme-suisses/

**Licence :** CC BY 4.0. Réutilisation libre, y compris commerciale, avec
mention de la source et un lien vers la page de l'étude.

La méthode, les définitions et les limites sont celles de la page de l'étude.
Les colonnes des fichiers CSV sont en anglais ; le fichier
`data/etude-pme-2026.json` garde les clés françaises et les définitions
d'origine.
