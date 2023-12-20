# papermill-nbconvert-report

Minimal example of using papermill and nbconvert to automate generating parametrized PDF reports


## Setup

Use following steps to setup the conda env:

```bash
conda create -n papermill-nbconvert-report python=3.10 -y
conda activate papermill-nbconvert-report
pip install -r requirements.txt
playwright install chromium
```

## Render

Example rendering of multiple reports by region and time frame. Could automate by calling commands with `subprocess` in Python or similar, or use `papermill` and `nbconvert` as packaged code in a driving script for your rendering needs.

See: https://papermill.readthedocs.io/en/latest/usage-execute.html#execute-via-the-python-api, https://nbconvert.readthedocs.io/en/latest/nbconvert_library.html

Can mix injecting parameters from command line, or YAML as needed.

Using Git Bash on Windows/Linux:
```bash
for region in USA Canada Mexico; do for year in 2019 2020 2021; do papermill template_report.ipynb -p location $region -f "configs/$year.yaml" | jupyter nbconvert --to webpdf --no-input --stdin --output "output/$region-$year"; done; done
```

This will output PDFs to `output/` directory.