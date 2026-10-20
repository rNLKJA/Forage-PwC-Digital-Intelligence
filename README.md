# Forage · PwC Switzerland Digital Intelligence

My work from the [PwC Switzerland Digital Intelligence job simulation](https://www.theforage.com/simulations/pwc-ch/digital-intelligence-kmu8) on Forage, completed in August 2023.

In the Responsible AI module, a bank wanted to know how a model that picks clients to call about term deposits reaches its decisions. The task was to build a classifier and explain which features drive its predictions, both across all clients and for two named clients. This repo holds my notebook for that module. The simulation lists other modules, but I did not keep work for them.

## What is in this repo

| Path | What it is |
| --- | --- |
| `responsible-ai.ipynb` | My notebook. It trains a cross-validated logistic regression on the UCI Bank Marketing data, checks it with a confusion matrix and a classification report, and explains it with SHAP. |
| `requirements.txt` | The Python packages the notebook imports. |
| `data/README.md` | Where to put the data file before running the notebook. |

## What I found

The model reached 0.90 accuracy on a held-out 20% of the data (8,238 calls). It found 38% of the clients who subscribed, and 67% of the clients it flagged did subscribe.

Across the test set, SHAP ranked call duration as the strongest feature, followed by the number employed (`nr.employed`) and the employment variation rate (`emp.var.rate`). For observations #4 and #20 the economic indicators led. `nr.employed` and `euribor3m` carried the most weight for both clients, with `pdays` next for #4 and `emp.var.rate` next for #20.

## Looking back

Two things stand out when I read this notebook again. About 88% of the test calls ended without a subscription, so 0.90 accuracy is only a little better than always predicting "no". I also kept call duration as a feature, and the UCI notes warn that duration is only known once the call is over. For a real calling list I would drop it, report results next to a simple baseline and explain the model again.

## Running the notebook

1. Download `bank-additional.zip` from the [UCI Bank Marketing page](https://archive.ics.uci.edu/dataset/222/bank+marketing) and copy `bank-additional-full.csv` into `data/`.
2. Install the packages with `pip install -r requirements.txt`.
3. Open `responsible-ai.ipynb` in Jupyter and run the cells in order.

The SHAP force plots for single clients are drawn with JavaScript, so they only show in a live Jupyter session. I cleared them from the saved notebook, along with the outputs that printed rows of the data.

## What is not in this repo

I left out everything that was not my own work. That covers the Forage task brief, the bank marketing data, the example notebook and pre-trained model that came with the programme, and the PwC report shared as background reading.

## Data and licence

The UCI Bank Marketing data set is by Moro, Cortez and Rita (2014) and is published by the UCI Machine Learning Repository under CC BY 4.0. Please download it from the source.

My code and writing in this repo are under the [MIT licence](LICENSE). The licence does not cover the data, the Forage brief or any PwC material, and none of those are included here.
