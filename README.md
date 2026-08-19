```
abdullah al-nafisah · llm inference hardware for commodity fpgas
```

I take the matrix–vector multiply that dominates every transformer linear layer,
push it into FPGA fabric, and then prove it matches the reference **bit for bit
on real silicon** — not in simulation, not within tolerance. Zero.

```
             one weight-stationary GEMV, four datapaths
            ┌──────────────────────────────────────────┐
AXI4-Stream ┤  Q4.12  ·  INT8  ·  W3 g128  ·  ternary  ├──> tokens
            └──────────────────────────────────────────┘
              microGPT  GPT-2    TinyLlama    BitNet
                ~KB     124 M      1.1 B      ~700 M

                       all on a $99 Zynq-7020
```

Same AXI-Stream boundary every time; only the datapath changes. That is the
whole thesis — the RTL ports up to a Kria K26 or a ZCU104 untouched.

### What that buys

| | model | quant | the part that shouldn't work |
|---|---|---|---|
| **INT8** | GPT-2 small · 124 M | per-channel INT8 | `0 / 220` DSP48E1 — every multiply inferred into LUTs · `max\|diff\| = 0` on 4/4 shapes |
| **W3** | TinyLlama-1.1B | W3 g128 AutoGPTQ | 1.1 B parameters living in a 512 MB board · 5/5 fixtures byte-exact **on the bitstream** |
| **ternary** | BitNet b1.58 · ~700 M | `{-1, 0, +1}` @ 2-bit | no multipliers at all — a mux-adder tree · 32 weights per 64-bit beat |

Ternary is the interesting one: because the weights are `{-1, 0, +1}`, every
multiply collapses to a sign-select and an add. There is no `*` anywhere in the
datapath, which lifts a 700 M model's decode ceiling from 2.8 to 11.4 tok/s at
the board's measured 1.99 GB/s.

> Deliberately **not** claimed: that any of this is faster than a CPU (it isn't),
> or that a model "runs on the FPGA" (the GEMVs do; norms, softmax and sampling
> run on the ARM). The defensible claims are bit-exactness, zero DSPs, and ~2.5 W.

### Nothing counts until it closes

A kernel isn't finished when it simulates. It's finished when the same golden
vectors come back off the board matching the reference exactly:

```
spec ──> SystemVerilog / HLS C++
             │
             ├──> Verilator · cocotb · C-sim
             ├──> golden fixtures, byte-exact
             ├──> bitstream, timing closed
             └──> silicon ──> max|diff| = 0
```

### Before this

Physics + EE at KFUPM, MSc ECE at KAUST. I worked on faster-than-Nyquist
signaling — packing symbols tighter than Nyquist and paying for it with a
turbo-equalized BCJR receiver that iterates its way back to clean bits.

**[coded-msprs](https://github.com/AbdullahAlNafisah/coded-msprs)** — rate-2
multi-stream partial-response signaling, AFF3CT simulation chain · [arXiv:2511.08553](https://arxiv.org/abs/2511.08553)

---

[**al-nafisah.com**](https://al-nafisah.com) · [Scholar](https://scholar.google.com/citations?user=_0BgAygAAAAJ&hl=en) · [ORCID](https://orcid.org/0000-0002-9537-1335) · [LinkedIn](https://www.linkedin.com/in/abdullah-al-nafisah/)
