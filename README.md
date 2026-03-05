# Microsoft Sentinel Workbooks

A collection of Azure Monitor Workbooks for Microsoft Sentinel cost analysis and optimization.

---

## Sentinel Ingest Cost Analysis

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fnemesis1286%2Fsentinel-workbooks%2Fmain%2FWorkbooks%2FSentinel-Ingest-Cost.json)

### Overview

This workbook provides a detailed breakdown of Microsoft Sentinel log ingestion costs split by **tier** — Analytics and Data Lake (Auxiliary/Basic). It helps you understand where your ingestion spend is going, identify high-volume tables, and evaluate whether moving certain tables to the Data Lake tier could reduce costs.

> **Note:** Default pricing reflects East US Pay-As-You-Go rates. Adjust the per-GB parameters to match your region, commitment tier, or EA/MCA pricing agreement.

### Features

- **Ingestion Cost Summary** — Side-by-side tile view of Analytics GB/cost, Data Lake GB/cost, and combined totals
- **Analytics Tier Breakdown** — Per-table ingestion volume and estimated cost, top-10 pie chart, and daily trend
- **Data Lake Tier Breakdown** — Per-table ingestion volume and estimated cost, top-10 pie chart, table type/retention info, and daily trend
- **Cost Optimization Insights**
  - What-If analysis: top 15 Analytics tables ranked by potential savings if moved to Data Lake
  - Commitment Tier Comparison: projects monthly spend across PAYG and 100/200/500 GB/day commitment tiers based on your average daily ingestion

### Parameters

| Parameter | Description | Default |
|---|---|---|
| Subscription | Azure subscription containing your Sentinel workspace | Auto-detected |
| Workspace | Log Analytics workspace linked to Sentinel | Auto-detected |
| Time Range | Query window (Last 24h / 7d / 30d / 90d or custom) | Last 30 days |
| Analytics Tier — Cost per GB | Simplified per-GB rate for Analytics ingestion | $4.30 (East US PAYG) |
| Data Lake Tier — Cost per GB | Per-GB rate for Basic/Auxiliary plan ingestion | $0.15 (East US) |
| Data Lake Tier Tables | Comma-separated list of tables on Basic or Auxiliary plans (auto-detected from workspace API) | Auto-detected |

### Deployment

#### Option 1 — Deploy to Azure (ARM Template)

Click the **Deploy to Azure** button above. The ARM template (`Workbooks/Sentinel-Ingest-Cost.json`) will deploy the workbook directly into your Azure subscription as a shared workbook under `microsoft.insights/workbooks`.

#### Option 2 — Manual Import

1. Open the [Azure Portal](https://portal.azure.com) and navigate to **Microsoft Sentinel**
2. Select your workspace, then go to **Workbooks** > **Add workbook**
3. Click the **Edit** button (pencil icon), then the **Advanced Editor** button (`</>`)
4. Paste the contents of `Workbooks/Sentinel-Ingest-Cost.workbook` and click **Apply**
5. Save the workbook to your workspace

### Files

| File | Description |
|---|---|
| `Workbooks/Sentinel-Ingest-Cost.json` | ARM deployment template — use with the Deploy to Azure button or `az deployment group create` |
| `Workbooks/Sentinel-Ingest-Cost.workbook` | Raw workbook JSON — use for manual import via the Azure Portal workbook editor |

### Requirements

- Microsoft Sentinel enabled on a Log Analytics workspace
- Reader access to the workspace and subscription
- The `Usage` table must be present and actively receiving data

### Pricing Reference

- [Azure Monitor / Log Analytics pricing](https://azure.microsoft.com/pricing/details/monitor/)
- [Microsoft Sentinel pricing](https://azure.microsoft.com/pricing/details/microsoft-sentinel/)
