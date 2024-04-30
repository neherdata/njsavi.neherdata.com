```python
## Reference links:
# https://dev.socrata.com/foundry/data.nj.gov/tfhb-8beb 
# https://data.nj.gov/stories/s/NJSAVI-Dataset-Story/9k98-6fqb/ 

###################
## DATASETS USED ##
###################

## yiaw-wr5c = out_of_state_businesses_certified_in_nj_by_state
# https://data.nj.gov/resource/yiaw-wr5c.json
# https://data.nj.gov/resource/yiaw-wr5c.csv

## tfhb-8beb = sbe
# https://data.nj.gov/resource/tfhb-8beb.json
# https://data.nj.gov/resource/tfhb-8beb.csv

## 8anu-hsjm = nj_certified_businesses
# https://data.nj.gov/resource/8anu-hsjm.json
# https://data.nj.gov/resource/8anu-hsjm.csv
```


```python
import pandas as pd
from sodapy import Socrata
import env
```


```python
# import app_token from env.py, create using env-template.py
app_token = env.app_token
```


```python
# Unauthenticated client only works with public data sets. Note 'None'
# in place of application token, and no username or password:
# client = Socrata("data.nj.gov", None)

# Example authenticated client (needed for non-public datasets):
client = Socrata("data.nj.gov", app_token=app_token)
```


```python
# Returned as JSON from API / converted to Python list of
# dictionaries by sodapy.
sbe = client.get("tfhb-8beb")
out_of_state_businesses_certified_in_nj_by_state = client.get("yiaw-wr5c")
nj_certified_businesses = client.get("8anu-hsjm")
```


```python
# Convert to pandas DataFrame
sbe_df = pd.DataFrame.from_records(sbe)
sbe_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>business_name</th>
      <th>business_address</th>
      <th>business_city</th>
      <th>business_state</th>
      <th>business_zip</th>
      <th>contact_name</th>
      <th>primary_phone</th>
      <th>email_address</th>
      <th>major_field_of_operation</th>
      <th>certification_type</th>
      <th>commodity_type</th>
      <th>commodity_code_description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BTNJ, LLC (AKA) POWER &amp; AUTOMATION ELECTRICAL ...</td>
      <td>851 VAN HOUTEN AVE</td>
      <td>CLIFTON</td>
      <td>NJ</td>
      <td>7013</td>
      <td>JOSEPH CASCIANO</td>
      <td>(973)777-4701</td>
      <td>NOLIVEIRA@POWERANDAUTOMATION.COM</td>
      <td>INDUSTRIAL ELECTRIC CONTRACTOR MAINLY PROVIDIN...</td>
      <td>SBE</td>
      <td>CONSTRUCTION CRAFT</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>WICKERSHEIM &amp; SONS, INC. (AKA) WICKERSHEIM &amp; S...</td>
      <td>92 FAIRMOUNT AVE.</td>
      <td>HACKENSACK</td>
      <td>NJ</td>
      <td>7601</td>
      <td>ROBERT WICKERSHEIM</td>
      <td>(201)343-4157</td>
      <td>INFO@WICKERSHEIMPLUMBING.COM</td>
      <td>PLUMBING, HEATING AND AIR CONDITIONING SERVICE...</td>
      <td>SBE</td>
      <td>CONSTRUCTION CRAFT</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GALIA CONSTRUCTION, INC.</td>
      <td>94 GORDON AVENUE</td>
      <td>TOTOWA</td>
      <td>NJ</td>
      <td>7512</td>
      <td>ELIZABETA BOSKOVSKI</td>
      <td>(973)897-4450</td>
      <td>GALIACONSTRUCTION@YAHOO.COM</td>
      <td>GALIA CONSTRUCTION, INC. IS CONCENTRATED IN RE...</td>
      <td>SBE</td>
      <td>CONSTRUCTION CRAFT</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ASSUNCAO BROS., INC. (AKA) ASSUNCAO BROTHERS</td>
      <td>29 WOOD AVE</td>
      <td>EDISON</td>
      <td>NJ</td>
      <td>8820</td>
      <td>MARTIN ASSUNCAO</td>
      <td>(732)549-8582</td>
      <td>GARRETT@ASSUNCAOBROTHERS.COM</td>
      <td>HEAVY HIGHWAY CONSTRUCTION, CONCRETE FLATWORK</td>
      <td>SBE</td>
      <td>CONSTRUCTION CRAFT</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>EASTERN ALLIANCE LLC</td>
      <td>400 GOFFLE RD</td>
      <td>HAWTHORNE</td>
      <td>NJ</td>
      <td>7506</td>
      <td>MATTHEW JACKOWITZ</td>
      <td>(201)543-4352</td>
      <td>MATT.JACKOWITZ@EASTALLIANCE.COM</td>
      <td>EASTERN ALLIANCE LLC IS A GC PERFORMING TELECO...</td>
      <td>SBE</td>
      <td>CONSTRUCTION CRAFT</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>995</th>
      <td>ROBOTECH CAD SOLUTIONS, INC.</td>
      <td>2 MARINE VIEW PLAZA</td>
      <td>HOBOKEN</td>
      <td>NJ</td>
      <td>7030</td>
      <td>SHLOMO MAROM</td>
      <td>(201)792-6300</td>
      <td>SHLOMO@ROBOTECHCAD.COM</td>
      <td>COMPUTER AIDED DESIGN (CAD), BUILDING INFORMAT...</td>
      <td>SBE</td>
      <td>CONSTRUCTION CRAFT  |  COMMODITY</td>
      <td>PLOTTERS, GRAPHIC  |  ARCHITECTURAL SOFTWARE, ...</td>
    </tr>
    <tr>
      <th>996</th>
      <td>INDUSTRIAL/COMMERCIAL CLEANING GROUP, INC.</td>
      <td>14 SOUTH BURNT MILL ROAD</td>
      <td>VOORHEES</td>
      <td>NJ</td>
      <td>8043</td>
      <td>KIM JORDAN</td>
      <td>(856)541-7241</td>
      <td>KJORDAN@ICCGRPINC.COM</td>
      <td>FACILITIES SUPPORT SERVICES</td>
      <td>SBE</td>
      <td>CONSTRUCTION CRAFT  |  COMMODITY</td>
      <td>AGRICULTURAL CROPS AND GRAINS, PURCHASED LOCAL...</td>
    </tr>
    <tr>
      <th>997</th>
      <td>SERVICE SUPPORT SPECIALTIES, INC. (AKA) S-CUBED</td>
      <td>6 MARS COURT</td>
      <td>MONTVILLE</td>
      <td>NJ</td>
      <td>7045</td>
      <td>GARY HILLMAN</td>
      <td>(973)263-0640</td>
      <td>GARYH@S-CUBED.COM</td>
      <td>SUPPLIER OF SEMICONDUCTOR MACHINERY AND PARTS</td>
      <td>SBE</td>
      <td>CONSTRUCTION CRAFT  |  COMMODITY</td>
      <td>ACTUATORS AND CONTROLS: ROBOTICS, SERVO SYSTEM...</td>
    </tr>
    <tr>
      <th>998</th>
      <td>PSP CONSTRUCTION, INC.</td>
      <td>38 ELIZABETH ST</td>
      <td>HACKENSACK</td>
      <td>NJ</td>
      <td>7601</td>
      <td>HARESH SAVALIA</td>
      <td>(917)299-5157</td>
      <td>PSPCONSSTRUCTION@YAHOO.COM</td>
      <td>GENERAL AND HEAVY CONSTRUCTION.</td>
      <td>SBE</td>
      <td>CONSTRUCTION CRAFT  |  COMMODITY</td>
      <td>CONSTRUCTION SERVICES, HEAVY, INCLUDING MAINTE...</td>
    </tr>
    <tr>
      <th>999</th>
      <td>LAMANNA ELECTRIC INC.</td>
      <td>10 WEST MANOR WAY</td>
      <td>ROBBINSVILLE</td>
      <td>NJ</td>
      <td>8691</td>
      <td>CHARLES LAMANNA JR</td>
      <td>(609)259-6282</td>
      <td>DEBBIER@LAMANNAELECTRIC.COM</td>
      <td>ELECTRICAL CONTRACTOR</td>
      <td>SBE</td>
      <td>CONSTRUCTION CRAFT  |  COMMODITY</td>
      <td>ACOUSTICAL TILE, INSULATING MATERIALS, AND SUP...</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 12 columns</p>
</div>




```python
# Convert to pandas DataFrame
out_of_state_businesses_certified_in_nj_by_state_df = pd.DataFrame.from_records(out_of_state_businesses_certified_in_nj_by_state)
out_of_state_businesses_certified_in_nj_by_state_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>business_name</th>
      <th>business_address</th>
      <th>business_city</th>
      <th>business_state</th>
      <th>business_zip</th>
      <th>contact_name</th>
      <th>primary_phone</th>
      <th>email_address</th>
      <th>major_field_of_operation</th>
      <th>commodity_code_description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>STAATS, AIMEE (AKA) DAKOTA CONSULTING</td>
      <td>8761 BLUFF LANE</td>
      <td>FAIR OAKS</td>
      <td>CA</td>
      <td>95628</td>
      <td>AIMEE STAATS</td>
      <td>(916)642-9410</td>
      <td>APSTAATS@GMAIL.COM</td>
      <td>MANAGEMENT CONSULTING, PROPOSAL MANAGEMENT, RE...</td>
      <td>MANAGEMENT CONSULTING</td>
    </tr>
    <tr>
      <th>1</th>
      <td>INTUEOR CONSULTING INC</td>
      <td>7700 IRVINE CENTER DRIVE, STE 610</td>
      <td>IRVINE</td>
      <td>CA</td>
      <td>92618</td>
      <td>VIJENDER MIDIDADDI</td>
      <td>(949)466-5663</td>
      <td>MIDIDADDI@INTUEOR.COM</td>
      <td>INTUEOR IS A STRATEGY, MANAGEMENT, AND TECHNOL...</td>
      <td>MANAGEMENT CONSULTING</td>
    </tr>
    <tr>
      <th>2</th>
      <td>LOTUS NEW JERSEY LLC (AKA) LOTUS NEW JERSEY LLC</td>
      <td>38 MOSS STREET, UNIT B103</td>
      <td>SAN FRANCISCO</td>
      <td>CA</td>
      <td>94103</td>
      <td>PHUONG TRAN</td>
      <td>(415)235-1388</td>
      <td>JOSHUABLACK33@GMAIL.COM</td>
      <td>APPLYING FOR LEGAL AND LICENSED RETAIL CANNABI...</td>
      <td>MISCELLANEOUS PRODUCTS (NOT OTHERWISE CLASSIFI...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>MAKE GREEN GO, INC.</td>
      <td>405 MORELLO DR</td>
      <td>HAYWARD</td>
      <td>CA</td>
      <td>94541</td>
      <td>LA WANDA KNOX</td>
      <td>(510)255-4669</td>
      <td>LAWANDA@MAKEGREENGO.COM</td>
      <td>ONLINE EDUCATION AND TRAINING, CURRICULUM DEVE...</td>
      <td>CONSULTING SERVICES  |  ADMINISTRATIVE CONSULT...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>EXAVALU, INC. (AKA) EXAVALU</td>
      <td>5000 BIRCH STREET, WEST TOWER, SUITE 3000</td>
      <td>NEWPORT BEACH</td>
      <td>CA</td>
      <td>92660</td>
      <td>REFIK ONGUN</td>
      <td>(310)245-2855</td>
      <td>ACCOUNTING@EXAVALU.COM</td>
      <td>INFORMATION TECHNOLOGY CONSULTING SERVICES</td>
      <td>CONSULTING SERVICES</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>420</th>
      <td>ASTYRA CORPORATION</td>
      <td>411 FRANKLIN STREET, SUITE 105</td>
      <td>RICHMOND</td>
      <td>VA</td>
      <td>23219</td>
      <td>KENNETH AMPY</td>
      <td>(804)433-1100</td>
      <td>REMIT@ASTYRA.COM</td>
      <td>STAFFING AGENCY</td>
      <td>GEOGRAPHIC INFORMATION SYSTEMS (GIS)  |  OFFIC...</td>
    </tr>
    <tr>
      <th>421</th>
      <td>OAKTON INFRASTRUCTURE SOLUTIONS LLC (AKA) OAKT...</td>
      <td>3000 PHYLLMAR PLACE</td>
      <td>OAKTON</td>
      <td>VA</td>
      <td>22124</td>
      <td>PRAVEEN MATHEWS</td>
      <td>(516)780-5060</td>
      <td>PRAVEEN@OAKTONIS.COM</td>
      <td>CONSULTING SERVICES IN ENERGY CONSERVATION AND...</td>
      <td>ENERGY CONSERVATION SERVICES, INCLUDING AUDITS</td>
    </tr>
    <tr>
      <th>422</th>
      <td>WIZZY'S NJ LLC</td>
      <td>500 106TH AVE. NE #1801</td>
      <td>BELLEVUE</td>
      <td>WA</td>
      <td>98004</td>
      <td>ZOYA VOLYNSKY</td>
      <td>(206)601-3598</td>
      <td>ZOYA@BELLEVUEHILLS.COM</td>
      <td>CANNABIS ESTABLISHMENT</td>
      <td>DRUGS AND PHARMACEUTICALS  |  MISCELLANEOUS PR...</td>
    </tr>
    <tr>
      <th>423</th>
      <td>HIGHER LEAF LLC</td>
      <td>13611 NE 8TH STREET, UNIT 207</td>
      <td>BELLEVUE</td>
      <td>WA</td>
      <td>98005</td>
      <td>MIRA ILYAGUYEV</td>
      <td>(425)445-9925</td>
      <td>MIRAZDY@HOTMAIL.COM</td>
      <td>CANNABIS ESTABLISHMENT</td>
      <td>DRUGS AND PHARMACEUTICALS  |  MISCELLANEOUS PR...</td>
    </tr>
    <tr>
      <th>424</th>
      <td>ILLUME ADVISING LLC (AKA) ILLUME ADVISING, LLC</td>
      <td>440 SCIENCE DRIVE, SUITE 202</td>
      <td>MADISON</td>
      <td>WI</td>
      <td>53711</td>
      <td>ALYSSA PRICE</td>
      <td>(608)807-2061</td>
      <td>ALYSSA@ILLUMEADVISING.COM</td>
      <td>ILLUME ADVISING IS A WHOLLY WOMAN-OWNED RESEAR...</td>
      <td>ENERGY CONSERVATION SERVICES, INCLUDING AUDITS...</td>
    </tr>
  </tbody>
</table>
<p>425 rows × 10 columns</p>
</div>




```python
nj_certified_businesses_df = pd.DataFrame.from_records(nj_certified_businesses)
nj_certified_businesses_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>business_name</th>
      <th>business_address</th>
      <th>business_city</th>
      <th>business_state</th>
      <th>business_zip</th>
      <th>contact_name</th>
      <th>primary_phone</th>
      <th>email_address</th>
      <th>major_field_of_operation</th>
      <th>commodity_code_description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BTNJ, LLC (AKA) POWER &amp; AUTOMATION ELECTRICAL ...</td>
      <td>851 VAN HOUTEN AVE</td>
      <td>CLIFTON</td>
      <td>NJ</td>
      <td>7013</td>
      <td>JOSEPH CASCIANO</td>
      <td>(973)777-4701</td>
      <td>NOLIVEIRA@POWERANDAUTOMATION.COM</td>
      <td>INDUSTRIAL ELECTRIC CONTRACTOR MAINLY PROVIDIN...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>WICKERSHEIM &amp; SONS, INC. (AKA) WICKERSHEIM &amp; S...</td>
      <td>92 FAIRMOUNT AVE.</td>
      <td>HACKENSACK</td>
      <td>NJ</td>
      <td>7601</td>
      <td>ROBERT WICKERSHEIM</td>
      <td>(201)343-4157</td>
      <td>INFO@WICKERSHEIMPLUMBING.COM</td>
      <td>PLUMBING, HEATING AND AIR CONDITIONING SERVICE...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GALIA CONSTRUCTION, INC.</td>
      <td>94 GORDON AVENUE</td>
      <td>TOTOWA</td>
      <td>NJ</td>
      <td>7512</td>
      <td>ELIZABETA BOSKOVSKI</td>
      <td>(973)897-4450</td>
      <td>GALIACONSTRUCTION@YAHOO.COM</td>
      <td>GALIA CONSTRUCTION, INC. IS CONCENTRATED IN RE...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ASSUNCAO BROS., INC. (AKA) ASSUNCAO BROTHERS</td>
      <td>29 WOOD AVE</td>
      <td>EDISON</td>
      <td>NJ</td>
      <td>8820</td>
      <td>MARTIN ASSUNCAO</td>
      <td>(732)549-8582</td>
      <td>GARRETT@ASSUNCAOBROTHERS.COM</td>
      <td>HEAVY HIGHWAY CONSTRUCTION, CONCRETE FLATWORK</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>EASTERN ALLIANCE LLC</td>
      <td>400 GOFFLE RD</td>
      <td>HAWTHORNE</td>
      <td>NJ</td>
      <td>7506</td>
      <td>MATTHEW JACKOWITZ</td>
      <td>(201)543-4352</td>
      <td>MATT.JACKOWITZ@EASTALLIANCE.COM</td>
      <td>EASTERN ALLIANCE LLC IS A GC PERFORMING TELECO...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>995</th>
      <td>ROBOTECH CAD SOLUTIONS, INC.</td>
      <td>2 MARINE VIEW PLAZA</td>
      <td>HOBOKEN</td>
      <td>NJ</td>
      <td>7030</td>
      <td>SHLOMO MAROM</td>
      <td>(201)792-6300</td>
      <td>SHLOMO@ROBOTECHCAD.COM</td>
      <td>COMPUTER AIDED DESIGN (CAD), BUILDING INFORMAT...</td>
      <td>PLOTTERS, GRAPHIC  |  ARCHITECTURAL SOFTWARE, ...</td>
    </tr>
    <tr>
      <th>996</th>
      <td>INDUSTRIAL/COMMERCIAL CLEANING GROUP, INC.</td>
      <td>14 SOUTH BURNT MILL ROAD</td>
      <td>VOORHEES</td>
      <td>NJ</td>
      <td>8043</td>
      <td>KIM JORDAN</td>
      <td>(856)541-7241</td>
      <td>KJORDAN@ICCGRPINC.COM</td>
      <td>FACILITIES SUPPORT SERVICES</td>
      <td>AGRICULTURAL CROPS AND GRAINS, PURCHASED LOCAL...</td>
    </tr>
    <tr>
      <th>997</th>
      <td>SERVICE SUPPORT SPECIALTIES, INC. (AKA) S-CUBED</td>
      <td>6 MARS COURT</td>
      <td>MONTVILLE</td>
      <td>NJ</td>
      <td>7045</td>
      <td>GARY HILLMAN</td>
      <td>(973)263-0640</td>
      <td>GARYH@S-CUBED.COM</td>
      <td>SUPPLIER OF SEMICONDUCTOR MACHINERY AND PARTS</td>
      <td>ACTUATORS AND CONTROLS: ROBOTICS, SERVO SYSTEM...</td>
    </tr>
    <tr>
      <th>998</th>
      <td>PSP CONSTRUCTION, INC.</td>
      <td>38 ELIZABETH ST</td>
      <td>HACKENSACK</td>
      <td>NJ</td>
      <td>7601</td>
      <td>HARESH SAVALIA</td>
      <td>(917)299-5157</td>
      <td>PSPCONSSTRUCTION@YAHOO.COM</td>
      <td>GENERAL AND HEAVY CONSTRUCTION.</td>
      <td>CONSTRUCTION SERVICES, HEAVY, INCLUDING MAINTE...</td>
    </tr>
    <tr>
      <th>999</th>
      <td>LAMANNA ELECTRIC INC.</td>
      <td>10 WEST MANOR WAY</td>
      <td>ROBBINSVILLE</td>
      <td>NJ</td>
      <td>8691</td>
      <td>CHARLES LAMANNA JR</td>
      <td>(609)259-6282</td>
      <td>DEBBIER@LAMANNAELECTRIC.COM</td>
      <td>ELECTRICAL CONTRACTOR</td>
      <td>ACOUSTICAL TILE, INSULATING MATERIALS, AND SUP...</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 10 columns</p>
</div>




```python

```
