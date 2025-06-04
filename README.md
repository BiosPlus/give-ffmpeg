# Give FFmpeg

This repository provides a [GitHub Actions](https://docs.github.com/en/actions) workflow that builds a static FFmpeg binary for Linux. The workflow checks out FFmpeg and several optional libraries and compiles them from source. Each dependency is cached to speed up future builds.

## Workflow overview

The workflow file is located at `.github/workflows/build-ffmpeg.yml` and contains multiple jobs:

- **dependency-svtav1** – compiles the SVT‑AV1 encoder
- **dependency-dav1d** – compiles the dav1d decoder
- **dependency-aom** – builds libaom
- **dependency-libvmaf** – builds libvmaf
- **dependency-libx264** – builds libx264
- **dependency-libx265** – builds libx265
- **dependency-libopus** – builds libopus
- **dependency-libvpx** – builds libvpx
- **build-ffmpeg** – runs after the dependencies are cached and compiles FFmpeg with the detected libraries enabled

Each job runs on Ubuntu and uses the [`actions/cache`](https://github.com/actions/cache) action so that subsequent runs reuse previously built artifacts.

## Running the workflow

The workflow triggers on pushes to `main` or when a pull request targets `main`. After the workflow completes, the resulting FFmpeg binary can be found in the job summary under **Artifacts**.

## Customising the build

To change the configuration flags or add more dependencies, edit the `build-ffmpeg.yml` file. The job named `Build FFmpeg` dynamically checks which libraries were successfully built and enables them when configuring FFmpeg. Additional libraries can be added following the existing pattern.

Currently the workflow targets `ubuntu-latest` on `x86_64`. Other architectures can be added by modifying the matrix values in the workflow file.

## Repository structure

```
.
├── .github/
│   └── workflows/
│       └── build-ffmpeg.yml  # GitHub Action to build FFmpeg
└── README.md
```

## License

No license file is present in this repository. If you plan to distribute binaries produced by this workflow, ensure that all included libraries are compatible with your chosen license.

