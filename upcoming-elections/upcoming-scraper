import requests
from bs4 import BeautifulSoup
import openpyxl
from openpyxl.styles import Alignment, Font, Border, Side, PatternFill
from openpyxl.utils import get_column_letter
import re

# Function to create and format an Excel file
def create_and_format_excel(page_name, candidates_data):
    wb = openpyxl.Workbook()
    ws = wb.active

    # Define cell styles
    header_style = Font(bold=True)
    cell_alignment = Alignment(wrap_text=True)

    # Define cell borders
    border = Border(left=Side(style='thin'), right=Side(style='thin'), top=Side(style='thin'), bottom=Side(style='thin'))

    # Create a new worksheet and apply styles to the header row
    ws.title = "Candidates Data"
    header_row = ["Election", "Election Link", "District", "Party", "Name", "Short Description", "Status", "Link"]
    ws.append(header_row)

    for cell in ws[1]:
        cell.font = header_style
        cell.alignment = cell_alignment
        cell.border = border
        cell.fill = PatternFill(start_color="D3D3D3", end_color="D3D3D3", fill_type="solid")

    # Add data to the worksheet
    for row_data in candidates_data:
        ws.append(row_data)
        for cell in ws[ws.max_row]:
            cell.alignment = cell_alignment
            cell.border = border

    # Auto-size columns based on content
    for column in ws.columns:
        max_length = 0
        column = [cell for cell in column]
        for cell in column:
            try:
                if len(str(cell.value)) > max_length:
                    max_length = len(cell.value)
            except:
                pass
        adjusted_width = (max_length + 2)
        ws.column_dimensions[get_column_letter(column[0].column)].width = adjusted_width

    # Save the Excel file with the page name
    file_name = f"{page_name}_Candidates.xlsx"
    wb.save(file_name)
    print(f"\x1b[32mExcel file '{file_name}' created successfully\x1b[0m")

# Function to check if a Wikipedia page exists for a specific URL
def wikipedia_page_exists(url):
    if url.startswith("https://en.wikipedia.org/wiki/"):
        response = requests.get(url)
        return response.status_code == 200
    return False

# Function to scrape candidate data from the Wikipedia page
def scrape_candidate_data(page_name):
    # Construct the URL based on the page name
    url = f"https://en.wikipedia.org/wiki/{page_name.replace(' ', '_')}"

    response = requests.get(url)

    if response.status_code == 200:
        soup = BeautifulSoup(response.text, 'html.parser')
        candidates_data = []

        sections = soup.find_all('span', {'class': 'mw-headline'})
        current_district = ""
        current_election = ""
        current_election_link = ""
        election_name = ""

        for section in sections:
            section_title = section.text.strip()

            if section_title.startswith("District "):
                current_district = section_title

                # Extract the election link from the {{main}} template
                main_template = soup.find('span', {'id': section.get('id')})
                if main_template:
                    hatnote = main_template.find_next('div', {'class': 'hatnote'})
                    if hatnote:
                        election_link_elem = hatnote.find('a', href=True)
                        current_election_link = "https://en.wikipedia.org" + election_link_elem['href'] if election_link_elem else ""
                        election_name = election_link_elem.text.strip()  # Extract the text of the link
                    else:
                        current_election_link = ""
                        election_name = ""
                else:
                    current_election_link = ""
                    election_name = ""

            if section_title.endswith(" primary"):
                current_election = section_title.replace(" primary", "")

            if current_district and current_election:
                if section_title == "Declared" or section_title == "Filed paperwork":
                    candidates_list = section.find_next('ul')

                    if candidates_list:
                        candidates = candidates_list.find_all('li')
                        for candidate in candidates:
                            # Extract the candidate's name and short description based on the text after the first comma
                            candidate_text = candidate.text.strip()
                            candidate_name, short_description = candidate_text.split(',', 1)
                            candidate_name = candidate_name.strip()
                            short_description = re.sub(r'\[\d+\]', '', short_description).strip()  # Remove square bracketed numbers
                            link = candidate.find('a', href=True)
                            if link and link['href'].startswith("/wiki/"):
                                candidate_link = "https://en.wikipedia.org" + link['href']
                                if wikipedia_page_exists(candidate_link):
                                    candidates_data.append([election_name, current_election_link, current_district, current_election, candidate_name, short_description, section_title, candidate_link])
                                else:
                                    candidates_data.append([election_name, current_election_link, current_district, current_election, candidate_name, short_description, section_title, "No Wikipedia Link Available"])
                            else:
                                candidates_data.append([election_name, current_election_link, current_district, current_election, candidate_name, short_description, section_title, "No Wikipedia Link Available"])

        create_and_format_excel(page_name, candidates_data)
    else:
        print(f"\x1b[91mFailed to retrieve the page for {page_name}.\x1b[0m")

# Ask the user for a list of Wikipedia page names (one per line)
print("Enter a list of Wikipedia page names (one per line). Type 'done' when finished.")
page_names = []
while True:
    page_name = input()
    if page_name.strip().lower() == 'done':
        break
    if page_name not in page_names:
        page_names.append(page_name)
    else:
        print(f"\x1b[91mSkipping duplicate page name:\x1b[0m {page_name}")

# Scrape candidate data for each page name
for page_name in page_names:
    scrape_candidate_data(page_name)

# Thank the user and credit the author
print("\n\x1b[37mThank you for using the Wikipedia scraper for upcoming elections.\x1b[0m")  # Light gray  
print("\x1b[37mAuthor: Gurwinder Singh\x1b[0m")  
print("\x1b[37mVersion: 1.0\x1b[0m")  
print("\x1b[37mFor any issues, please contacton on Upwork: freelancers/~0162de9053b9e180f4\x1b[0m") 
