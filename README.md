<table>
<tr>
<td valign="top" width="54%">

### abdullah al-nafisah

`signal processing, and the hardware that runs it`

Physics and Electrical Engineering at KFUPM. MSc in Electrical and Computer Engineering at KAUST.

`c++` `python` `systemverilog` `vitis hls` `cocotb` `pynq`

</td>
<td valign="top" width="46%">

<pre>
    ┌───────────────────────────┐
║█║ │                           │ ║█║
║█║ │  ┌─────────┐ ┌─────────┐  │ ║█║
║█║ │  │ ARM  PS │ │   PL    │  │ ║█║
║█║ │  │ softmax │ │  GEMV   │  │ ║█║
║█║ │  │ norms   │ │ ███████ │  │ ║█║
║█║ │  └─────────┘ └─────────┘  │ ║█║
║█║ │         XC7Z020           │ ║█║
    └───────────────────────────┘
</pre>

</td>
</tr>
</table>

### MS-PRS: two bits per symbol, then untangling them

Most radios send one symbol at a time and work hard to stop them smearing into each other. Multi-Stream Partial Response Signaling does the opposite. It adds the smearing deliberately, in the digital domain, through short filters across two sub-streams, and hands the receiver the job of undoing it. Nothing is compressed in time, which is what separates it from faster-than-Nyquist signaling.

Undoing it is a loop. A BCJR equalizer and an outer decoder pass soft guesses back and forth, each one sharpening the other's next pass, until the bits settle. At rate 2 this carries two bits per channel use, the same spectral efficiency as 4-ASK, on a four-state trellis when L0 = 3.

The simulator is C++ on AFF3CT with a Python reference beside it, and the two agree to better than 1e-6 on identical input. 414 cached BER points and 12 EXIT characteristics live in the repo, so every figure regenerates without rerunning a simulation.

**[coded-msprs](https://github.com/AbdullahAlNafisah/coded-msprs)** · [arXiv:2511.08553](https://arxiv.org/abs/2511.08553) · [MSc thesis, KAUST](https://repository.kaust.edu.sa/items/db129afb-21ad-468d-aaee-864f2518d0b7)

### Now: transformer inference on small FPGAs

Running language models on a $99 PYNQ-Z2 board by moving the matrix multiply that dominates every layer into programmable logic, and checking the result against the reference bit for bit on the board itself. Three sizes so far: GPT-2 124 M at INT8, TinyLlama-1.1B at 3 bits per weight, and a ternary kernel that needs no hardware multipliers at all.

These repositories are private while the work is early. Measured numbers, and what is deliberately not claimed, are on [al-nafisah.com](https://al-nafisah.com).

---

[**al-nafisah.com**](https://al-nafisah.com) · [Scholar](https://scholar.google.com/citations?user=_0BgAygAAAAJ&hl=en) · [ORCID](https://orcid.org/0000-0002-9537-1335) · [LinkedIn](https://www.linkedin.com/in/abdullah-al-nafisah/)
