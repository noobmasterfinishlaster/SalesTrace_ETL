# SalesTrace_ETL
## 🛠 Handling Auto-Increment (IDENTITY) Columns in SSIS

When loading data into a table with an IDENTITY column (e.g., `NAD_EU_XREF_ID` column of NAD_EU_XREF table), SSIS can't insert values into that column unless special handling is done.

### 🧩 Scenario
You have an IDENTITY column but want to insert your **own values** from the source file instead of letting SQL Server auto-generate.After I load the data fi a new data is being added the SQL server will auto generate the data

### ✅ Solution

1. **Turn ON Identity Insert using execute sql task** before data load:
   ```sql
   SET IDENTITY_INSERT [MDM_STAGE].[NAD_EU_XREF_NEW] ON;
2. **Connect the output with the data flow task**:
   Connect the output wiht data flow task , add the source , connect it with derived column and data conversion and then connect it with the ole db destination .
3. **Bit modification in the OLE DB DESTINATION**:
   Click on the advance editor of the OLE DB , Select Component Properties , Select FastLoadKeepIdentity and Turn it True .
3. **Turn off Identity Insert using execute sql task**:
   ```sql
   SET IDENTITY_INSERT [MDM_STAGE].[NAD_EU_XREF_NEW] ON;```
   
   also FastLoadKeepIdentity should also be turned into false 
