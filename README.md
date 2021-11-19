# Hacktribe
Electribe 2 hacks, based on sampler firmware version 2.02.

## Features
- Sampling
- Filters
- Oscillators
- More IFX
- More scales
- More grooves
- Custom init pattern
- Supports synth and sampler hardware

See [demo video](https://www.youtube.com/watch?v=n0wXUqgfa9Q) by [Thomas Herrmann](https://github.com/BKLronin).


## [How To](../../wiki/firmware-patch)

Clone the repo, including submodules:

    git clone --recursive https://github.com/bangcorrupt/hacktribe.git
    cd hacktribe

Download Electribe Sampler firmware version 2.02 and move `SYSTEM.VSB` to `hacktribe` directory

Apply patch to Electribe Sampler firmware version 2.02 only:

    sha256sum -c hash/SYSTEM.VSB.sha
    bspatch SYSTEM.VSB hacked-SYSTEM.VSB patch/hacktribe-2.patch
    sha256sum -c hash/hacked-SYSTEM.VSB.sha

Edit header if currently running synth firmware:
    
    python scripts/e2-header.py hacked-SYSTEM.VSB

Optionally, set custom init pattern:

    python scripts/e2s-init-pat.py hacked-SYSTEM.VSB init-pat.e2spat


Use `samples/hacktribe-blank-e2sSample.all` to free up sampling time.

## [What If?](../../wiki/debrick)

## License
Contents of `patch` and `samples` directories are not open source and are not covered the GPL.

All other files licensed AGPL-3.0 unless stated otherwise.
