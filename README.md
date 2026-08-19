<table>
<tr>
<td valign="top" width="54%">

### abdullah al-nafisah

`signal processing, and the hardware that runs it`

Physics and EE at KFUPM. MSc ECE at KAUST.

Agentic workflows, quantized LLM inference, and RTL that is machine-checked
before it counts.

[**CV**](cv/Abdullah_Al_Nafisah_CV.pdf)

</td>
<td valign="top" width="46%">

<pre>
   one network, three times

 float32  PyTorch
    │
    ├─ int8  quantizer   ┐
    ├─ int8  C++ / STM32 ├ byte
    └─ int8  RTL / FPGA  ┘ identical
</pre>

</td>
</tr>
</table>

**[nano-inference](https://github.com/AbdullahAlNafisah/nano-inference).** One integer network implemented three times, trained in PyTorch, quantized by hand, generated as C++ for an STM32 and as SystemVerilog for a PYNQ-Z2, and machine-checked byte-identical. It classifies a letter written in the air from a 6-axis IMU. In progress.

**Multi-Stream Partial Response Signaling.** Two bits per symbol, interference added on purpose, and a turbo loop that untangles it.
[coded-msprs](https://github.com/AbdullahAlNafisah/coded-msprs) · [arXiv:2511.08553](https://arxiv.org/abs/2511.08553) · [MSc thesis](https://repository.kaust.edu.sa/items/db129afb-21ad-468d-aaee-864f2518d0b7)

---

[**al-nafisah.com**](https://al-nafisah.com) · [Scholar](https://scholar.google.com/citations?user=_0BgAygAAAAJ&hl=en) · [ORCID](https://orcid.org/0000-0002-9537-1335) · [LinkedIn](https://www.linkedin.com/in/abdullah-al-nafisah/)
