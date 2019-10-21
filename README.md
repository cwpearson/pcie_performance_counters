* [opcm/pcm](https://github.com/opcm/pcm): a library / set of tools for monitoring performance counters
  * including PCIe
  * looks like this is the solution Intel recommends right now
  
  * PCIe read events (PCI devices reading from memory - application writes to disk/network/PCIe device)
    * PCIePRd: PCIe UC read transfer (partial cache line)
    * PCIeRdCur: PCIe read current transfer (full cache line). On Haswell Server PCIeRdCur counts both full/partial cache lines
    * RFO:      Demand Data RFO
    * CRd:      Demand Code Read
    * DRd:      Demand Data Read
    * PCIeNSWr: PCIe Non-snoop write transfer (partial cache line)
  * PCIe write events (PCI devices writing to memory - application reads from disk/network/PCIe device)
    * PCIeWiLF  - PCIe Write transfer (non-allocating) (full cache line)
    * PCIeItoM  - PCIe Write transfer (allocating) (full cache line)
    * PCIeNSWr  - PCIe Non-snoop write transfer (partial cache line)
    * PCIeNSWrF - PCIe Non-snoop write transfer (full cache line)
    * ItoM      - PCIe write full cache line
    * RFO       - PCIe partial Write
  * CPU MMIO events (CPU reading/writing to PCIe devices):
    * PRd       - MMIO Read [Haswell Server only] (Partial Cache Line)
    * WiL       - MMIO Write (Full/Partial)
  * Some additional info on p. 30 of Intel Xeon Processor E5-2600 Product Family Uncore Performance Monitoring Guide   ([pdf/repo](refs/xeon_e5_2600_uncore_guide.pdf))  ([intel.com](https://www.intel.com/content/dam/www/public/us/en/documents/design-guides/xeon-e5-2600-uncore-guide.pdf))
  
* [icl/papi](https://bitbucket.org/icl/papi/src/master/): a library for reading performance counters

* [pmu-tools/ucevent](https://github.com/andikleen/pmu-tools/tree/master/ucevent): a python tool for some uncore events, that uses the `/sys/...` filesystem

## References

* Intel 64 and IA-32 Architectures Software Developers Manual Volume 3 ([pdf/repo](refs/intel_sdm3.pdf)) ([intel.com](https://www.intel.com/content/www/us/en/architecture-and-technology/64-ia-32-architectures-software-developer-system-programming-manual-325384.html))
  * S 18, p. 641
  * S 19, p. 763

* Intel Xeon Processor E5-2600 Product Family Uncore Performance Monitoring Guide   ([pdf/repo](refs/xeon_e5_2600_uncore_guide.pdf))  ([intel.com](https://www.intel.com/content/dam/www/public/us/en/documents/design-guides/xeon-e5-2600-uncore-guide.pdf))

* [A 2015 blog post on pcm and PCIe performance counters](https://jdinkla.github.io/software-development/2015/04/24/measuring-traffic-on-the-pci-express-bus-pcie.html)
