# NotionToDocs — Use your Notion recipes with Gemini

Automatically sync your Notion recipes into a Google Document — no manual copying, always up to date, and instantly usable with Gemini.  
Access your recipes where you cook, on your smartphone, smartwatch, or tablet.  

## 📸 From Notion to Document (used with Gemini)
| Notion (Source) | Google Document | Gemini Recipe Suggestion |
|-----------------|-----------------|--------------------------|
| <img src="screenshots/recipes-notion.png" width="650"> | <img src="screenshots/recipes-google-doc.png" width="640"> | <img src="screenshots/recipe-suggestion-gemini.png" width="515"> |  

⭐ *If you find this useful, feel free to give it a star.*

## 🚀 Why you need it
Recipes are often scattered across different tools and require **manual copying** to use elsewhere.  
This project keeps everything automatically in sync in one structured place — so Gemini can always access and use your recipes.  
- All recipes in one place  
- **Automatically synced** (no manual updates)  
- Works directly with Gemini  
- Clean, structured format for AI  

## 🔗 How it connects
Notion (recipes) → **NotionToDocs** → Google Document → Gemini → your devices  
This automation keeps everything in sync automatically, so your recipes are always ready to use whenever you cook.  

## ⚙️ Overview
This project consists of two workflows:
* **Initial Sync** → builds the full document from scratch (runs daily)  
* **Incremental Sync** → updates only changed recipes (runs every minute)

*Scheduling can be adjusted easily in the nodes.*  

The system ensures:  
* consistent structure using markers
* efficient updates via incremental processing
* automatic cleanup of deleted entries

### Key Concepts
**Markers**  
Define sections in the document to safely replace content

**Incremental Updates**  
Only modified recipes are processed

**Cleanup Logic**  
Deleted recipes are removed from the document

## 🔄 Workflows
### Initial Sync
```text
→ Get recipes from Notion
→ Build new recipe content
→ Replace old with new content
```
#### Workflow Overview
<img src="screenshots/workflow-initial.png" width="800">

### Incremental Sync
```text
PREPARING AND GATHERING INFO
→ Fetch sync states & recipes 

CHECK & INSERT MARKERS
→ If marker not found → Insert
→ If marker found → Forward

CREATE NEW CONTENT
→ Get recipe data and wrap markers

CREATE OLD CONTENT
→ Get content from marker to marker

UPDATE DOCUMENT
→ Replace old and new content

CLEANUP DELETED RECIPES
→ Extract recipe IDs & sections
→ Identify already deleted recipes
→ Delete recipes in the document
```
#### Workflow Overview
<img src="screenshots/workflow-incremental.png" width="1200">

## 📊 Scaling and Performance
Tested with:
```text
500 recipes (fully populated)
```

**Important:**  
Large changes (> 50 recipe updates per minute) should be handled by the Initial Sync.  
The Incremental Sync is designed for quick updates.  

## 🛠️ Setup
1. Import workflows:
   * initial-setup.json  
   * incremental-sync.json  

2. Prepare Notion:
   * Create a database for your recipes  
   * Create an additional database called `NotionToDocs`  
   * Add a text property `lastSync`  
   *This database is used to store the last sync timestamp for incremental updates*

3. Connect credentials:
   * Notion  
   * Google Document API  

4. Run:
   * Execute Initial Sync once to build the document  

5. Activate workflows:
   * Activate Initial Sync (for daily runs)  
   * Activate Incremental Sync (for frequent updates)  

## 🧠 Use with Gemini
Once your Google Document is created, you can use it with Gemini inside your Google Workspace.  
On first use, Gemini will ask to connect your workspace — after that, your document is automatically available.  

You can then simply reference your recipes in a prompt, for example:
- "Show me recipes from my document"
- "Suggest a recipe based on these ingredients: ..."

Gemini will use your synced document to:
- search recipes  
- suggest meals based on ingredients  
- interact with your recipe collection  

*Gemini is the main use case — the sync also works independently.*

## 💡 Usage Tip
Include available ingredients (e.g. a short list or a fridge screenshot) when using the synchronized Google Document with Gemini for more relevant recipe suggestions.  

## 📄 License
MIT
