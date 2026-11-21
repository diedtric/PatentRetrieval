# U.S. Patent Allowances

A Streamlit dashboard for public U.S. patent applications with a mailed Notice
of Allowance in a selected seven-day window. The default ends yesterday in
Arizona. The chart, table and CSV export follow the same filters.

## Run locally

Use Python 3.11 or newer. From this directory, run:

```sh
python -m pip install -r requirements.txt
python -m streamlit run app.py
```

Open the URL printed in the terminal. Select **Demo data** to try the app with
fictional records. For live data, obtain an API key from the
[USPTO Open Data Portal](https://data.uspto.gov/), then enter it in the app's
password field. You can also set the `USPTO_API_KEY` environment variable
before starting Streamlit.

## Deploy on Streamlit Community Cloud

Push the extracted project files to a GitHub repository you administer. In
[Streamlit Community Cloud](https://share.streamlit.io/), choose **Create app**,
select the repository and branch, and set the entry point to `app.py`.
If you want visitors to bring their own key, leave the secret unset. To supply
a shared key, add this root-level setting in **Advanced settings → Secrets**:

```toml
USPTO_API_KEY = "your-key-here"
```

A shared key uses your USPTO quota. Keep the key out of GitHub.

## Data and downloads

- The app searches the [USPTO Patent File Wrapper API](https://data.uspto.gov/apis/patent-file-wrapper/search)
  by transaction code and date, then checks that both are on the same event.
  It counts one row per application per notice mailing date. Separate mailing
  dates for the same application appear as separate events.
- The mailing date is the event date for USPTO transaction code
  [MN/=.](https://www.uspto.gov/sites/default/files/documents/Appendix%20B_0.pdf).
  Current status and grant date are separate fields.
- Public coverage and indexing delays can affect results. The latest day may
  be incomplete. Refresh clears the 30-minute cache for the chosen week and key.
- Each record links to Patent Center. When the USPTO supplies the identifiers,
  the table also links to [published application and issued patent PDFs](https://www.uspto.gov/sites/default/files/documents/PDF-links-QRG-Patent-Public-Search.pdf).
  Use Patent Center for available file-wrapper documents, including the notice.
- The CSV contains the currently filtered records, including document links.
