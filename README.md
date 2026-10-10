# Berna R7 - Root Model

A **1.20B** multilingual language model with a modular cell-based architecture.

Berna R7 implements the **DNA-Kernel Plexus** architecture from Berna R5 (DOI: [10.5281/zenodo.23015308](https://doi.org/10.5281/zenodo.23015308)).

**Zenodo DOI:** [10.5281/zenodo.23037065](https://doi.org/10.5281/zenodo.23037065)  
**Mendeley DOI:** [10.17632/k24wwx6tp6.1](https://doi.org/10.17632/k24wwx6tp6.1)

- **Model:** 1.20B parameters, trained from scratch
- **Data:** 2.66B tokens (English + Math + Code)
- **Hardware:** 1x RTX 5090 (32 GB) → 1x A100 SXM (80 GB)
- **License:** Berna Research v1.0
- **Weights:** [muhamedkamil/berna-r7-v3](https://huggingface.co/muhamedkamil/berna-r7-v3)

## Status

| Component | Status |
|-----------|--------|
| Tokenizer (32k BPE) | ✅ complete |
| Data pipeline | ✅ complete (2.66B tokens) |
| Root model training | 🟢 in progress (step 2,790 / 10,200, loss 3.01) |
| Cell system (R5) | ✅ implemented (896 active / 1680 total) |
| H1 experiment (splitting) | ✅ tested (784 splits, 3 waves) |
| H2 experiment (forgetting) | ⏳ after Root |
| Baseline comparison | ⏳ after Root |
| Weights on HuggingFace | ✅ 7 checkpoints uploaded |

## Architecture

Berna R7 implements the six-layer structure from R5:

    Input → Sensors → Spinal Cord → Plexus → Knowledge Cells → DNA Kernel → Registry

- **Knowledge Cells:** 896 active / 1680 total (dynamic growth: 112 → 224 → 448 → 896)
- **6D Knowledge Vector:** K = [L, W, H, D, T, E], S = ||K||_omega
- **DNA Kernel:** 100 chromosomes × 4 genes
- **Plexus:** dynamic graph from co-activations
- **Registry:** SQL catalog of models and cells

See ARCHITECTURE.md and DNA.md for details.

## Cell Growth Dynamics

| Step | Active Cells | Event |
|------|--------------|-------|
| 0    | 112          | Initial |
| 300  | 224          | Split wave 1 |
| 600  | 448          | Split wave 2 |
| 900  | **896**      | Split wave 3 |
| 900+ | 896          | **Stable** (1700+ steps) |

**Growth factor:** 8x, then natural stop.  
**K6 Encompassment:** stable at 0.6138.  
**Births:** 0 (no novel patterns in current data).

## Project Structure

    berna-r7/
      ARCHITECTURE.md      system design
      DNA.md               DNA Kernel spec
      README.md            this file
      LICENSE              Berna Research v1.0
      code/
        cells/             cell lifecycle (R5 implementation)
        baselines/         vanilla, EWC, PackNet
        train.py           training entry point
        dataset.py         data loader
        eval.py            perplexity
        h1_saturation_experiment.py
        h2_forgetting_experiment.py
      registry/
        schema.sql         SQL schema
        rules.json         router rules
      paper/
        outline.md         planned paper

## Compliance with R5

| R5 Component | R7 Status |
|--------------|-----------|
| Registry + UUIDs | ✅ implemented |
| connection_token | ✅ implemented |
| Federation | ✅ implemented |
| from-scratch training | ✅ yes |
| Knowledge Cells | ✅ 896 active / 1680 total |
| 6D K vector | ✅ K1, K3, K5, K6 |
| DNA Kernel | ✅ 100×4 |
| S* = 0.85 | ✅ yes |
| Splitting (H1) | ✅ tested (784 splits) |
| Plexus | ✅ implemented |
| Router (Spinal Cord) | ⏳ deferred |
| Bounded Forgetting (H2) | ⏳ not yet tested |

## Citation

If you use Berna R7 in academic work:

    @software{berna_r7_2026,
      author    = {Muhammed, Mohammed Kamil},
      title     = {Berna R7: A 1.20B Multilingual Language Model},
      year      = {2026},
      publisher = {Berna Labs},
      url       = {https://github.com/Berna-Labs/berna-r7}
    }

For the underlying theory (R5):

    @software{berna_r5_2026,
      author    = {Muhammed, Mohammed Kamil},
      title     = {DNA-Kernel Plexus},
      year      = {2026},
      doi       = {10.5281/zenodo.23015308}
    }

## License

**Berna Research License v1.0** — see LICENSE.

Research use is free. Commercial use requires a separate license.

Contact: info@bernalabs.com
