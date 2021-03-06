About
=====

This holds a Statistical Packet Inspection system. Its divided into two parts: libspi - a backend handling the maths -
and spid - frontend deciding what to feed libspi with and what to do with the results.

libspi events
=============

Below is list of libspi events. They can be also treated as messages.

Subscribe to events with `spi_subscribe()`, announce with `spi_announce()`.

* `endpointPacketsReady(struct spi_ep *ep)` - endpoint accumulated at least C packets (default 80) and
  is ready for classification
* `endpointClassification(struct spi_classresult *cr)` - endpoint packets classified and new result ready
  for decision process
* `endpointVerdictChanged(struct spi_ep *ep)` - verdict about classification changed for this endpoint
* `traindataUpdated(void)` - new learning samples queued
* `classifierModelUpdated(void)` - some samples learned, the model database has changed
* `gcSuggestion(void)` - running garbage collector suggested
* `sourceClosed(struct spi_source *src)` - source finished and closed
* `finished(void)` - all sources finished, no learning pending and trainqueue empty

spid notes
==========

* detection is started after all offline learning sources are successfully completed, and if there are no interactive learning
  sources

For future work
===============

* libspi
  * better handling of unknown protocols in performance stats
  * better endpoint locking?
  * compute average size, IPT and jitter for both directions separately?
* spid
  * sooner or later a real config file will be necessary :)
  * better actions
