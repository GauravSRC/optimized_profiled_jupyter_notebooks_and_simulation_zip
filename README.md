Headline: per-spectrum latency at batch size 1 went from **377 ms** (autoregressive beam search) to **4.47 ms** (226 spectra/s), and **1,218 spectra/s** at batch size 512.

## Environment

NVIDIA L4 (23.6 GB) · PyTorch 2.7.1+cu128 · CUDA 12.8 · Casanovo v5.0.0 · depthcharge 0.4.10
Dataset: `multi-enzyme-simple.test.mgf` (106,933 spectra) --[Zenodo 12587317](https://zenodo.org/records/12587317)

## Notebooks

**Autoregressive baseline**
- [`ar.ipynb`](ar.ipynb)
- [`25 may final AR profiling.ipynb`](25%20may%20final%20AR%20profiling.ipynb)

**Non-autoregressive pipeline and optimization**
- [`nar1.ipynb`](nar1.ipynb)
- [`narcc1 (1).ipynb`](narcc1%20(1).ipynb)
- [`narbf16fa2_no_fa2.ipynb`](narbf16fa2_no_fa2.ipynb) --BF16 and FlashAttention
- [`tf32.ipynb`](tf32.ipynb) --TF32
- [`aot_inductor_failed_improvement.ipynb`](aot_inductor_failed_improvement.ipynb) --AOT Inductor, no improvement
- [`cpu_only_bs1_profiling.ipynb`](cpu_only_bs1_profiling.ipynb) --CPU-only baseline at bs=1
- [`depthcharge_fix_12ms_latency.ipynb`](depthcharge_fix_12ms_latency.ipynb) --depthcharge source fixes, 12.9 ms
- [`graph_breaks_4ms_final_optimization_fix.ipynb`](graph_breaks_4ms_final_optimization_fix.ipynb) --**final 4.47 ms result**

**AR FlashAttention work**
- [`ar_flash_testing.ipynb`](ar_flash_testing.ipynb)
- [`ar_profiling flash testing.ipynb`](ar_profiling%20flash%20testing.ipynb)
- [`ar_optimization_5000_final.ipynb`](ar_optimization_5000_final.ipynb) --end-to-end BF16 + multi-batch validation

**Streaming and real-time simulation**
- [`simulation_folder_zip_file_link`](simulation_folder_zip_file_link) --micro-batching simulator and real-time mzML replay

## Note

All numbers in these notebooks are **latency only**. No amino-acid or peptide-level accuracy has been measured, and the non-autoregressive results are architectural timing on an AR-trained checkpoint patched to run non-autoregressively --the timing is real, the predictions are not. 
