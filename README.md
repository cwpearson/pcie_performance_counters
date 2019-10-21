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
      * event 248 on SKX, corresponds to LLC_PCIE_DATA_BYTES on page 67/227 of the skylake uncore performance monitoring manual
    * RFO       - PCIe partial Write
  * CPU MMIO events (CPU reading/writing to PCIe devices):
    * PRd       - MMIO Read [Haswell Server only] (Partial Cache Line)
    * WiL       - MMIO Write (Full/Partial)
  * Some additional info on p. 30 of Intel Xeon Processor E5-2600 Product Family Uncore Performance Monitoring Guide   ([pdf/repo](refs/sandybridge_ep_uncore_guide.pdf))  ([intel.com](https://www.intel.com/content/dam/www/public/us/en/documents/design-guides/xeon-e5-2600-uncore-guide.pdf))


* [pmu-tools/ucevent](https://github.com/andikleen/pmu-tools/tree/master/ucevent): a python tool for some uncore events,wrapper around perf.
  * may have more data than pcm
  * The equations here seem to be taken from the Intel uncore performance monitoring manuals.
    * [Broadwell events](https://github.com/andikleen/pmu-tools/blob/master/ucevent/bdxde_uc.py): corresponding to [refs/broadwell_ep_ex_uncore_guide.pdf]
    * [Sandybridge Events](https://github.com/andikleen/pmu-tools/blob/master/ucevent/jkt_uc.py): corresponding to [refs/sandybridge_ep_uncore_guide.pdf]
    * [Skylake Events](https://github.com/andikleen/pmu-tools/blob/master/ucevent/skx_uc.py): corresponding to [refs/skylake_sp_uncore_guide.pdf]

  
* [icl/papi](https://bitbucket.org/icl/papi/src/master/): a library for reading performance counters
  * seems out of date

* perf:
  * perf stat -e 
  * http://www.bnikolic.co.uk/blog/hpc-prof-events.html
  * tough to figure out what event codes to give
  
  

## References

* Intel 64 and IA-32 Architectures Software Developers Manual Volume 3 ([pdf/repo](refs/intel_sdm3.pdf)) ([intel.com](https://www.intel.com/content/www/us/en/architecture-and-technology/64-ia-32-architectures-software-developer-system-programming-manual-325384.html))

* Intel uncore performance guides:
  * Sandy Bridge EP ([pdf/repo](refs/sandybridge_ep_uncore_guide.pdf))  ([intel.com](http://www.intel.com/content/dam/www/public/us/en/documents/design-guides/xeon-e5-2600-uncore-guide.pdf))
  * Broadwell EP/EX ([pdf/repo](refs/broadwell_ep_ex_uncore_guide.pdf))  ([intel.com](http://www.intel.com/content/www/us/en/processors/xeon/xeon-e5-e7-v4-uncore-performance-monitoring.html)) 
  * Skylake SP ([pdf/repo](refs/skylake_sp_uncore_guide.pdf))  ([intel.com](https://www.intel.com/content/www/us/en/processors/xeon/scalable/xeon-scalable-uncore-performance-monitoring-manual.html))


* [A 2015 blog post on pcm and PCIe performance counters](https://jdinkla.github.io/software-development/2015/04/24/measuring-traffic-on-the-pci-express-bus-pcie.html)

* [Intel Blog Post](https://software.intel.com/en-us/blogs/2014/07/11/documentation-for-uncore-performance-monitoring-units) describing uncore performance monitoring manuals for different archs

* [Intel List of Uncore Performance Monitoring Guides](https://software.intel.com/en-us/articles/intel-sdm#uncore): have to decode the arch from the product family name
