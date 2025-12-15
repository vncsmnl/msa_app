# MSA A-Star / PA-Star Flask Application

A web-based interface for running Multiple Sequence Alignment (MSA) using A-Star and PA-Star algorithms.

## Overview

This Flask application provides a user-friendly web interface for executing Multiple Sequence Alignment using optimized A-Star and Parallel A-Star (PA-Star) algorithms. It supports various benchmark sequence datasets and provides tools for managing sequences, binaries, and alignment results.

## Features

- **Multiple Algorithm Support**: Run MSA using A-Star or PA-Star implementations
- **Benchmark Datasets**: Built-in support for BALIBASE, Benchmark, NUC, and PAM250 sequence datasets
- **Binary Management**: Easy selection and management of different algorithm binaries
- **Sequence Management**: Browse and select FASTA sequences from organized datasets
- **Results Tracking**: View and manage alignment execution results
- **Parallel Processing**: Support for multi-threaded execution with configurable thread count
- **Cost Matrix Options**: Support for different substitution matrices (PAM250, etc.)
- **Web Interface**: Clean, intuitive web UI for all operations

## Project Structure

```
msa_app/
├── app.py                  # Application entry point
├── requirements.txt        # Python dependencies
├── app/
│   ├── __init__.py        # Flask app factory
│   ├── config.py          # Configuration settings
│   ├── routes/            # API routes
│   │   ├── binaries.py    # Binary management endpoints
│   │   ├── results.py     # Results viewing endpoints
│   │   ├── run.py         # Alignment execution endpoints
│   │   └── sequences.py   # Sequence browsing endpoints
│   ├── services/          # Business logic
│   │   ├── binaries_service.py
│   │   ├── results_service.py
│   │   ├── runner_service.py
│   │   └── sequences_service.py
│   ├── static/            # CSS and static assets
│   │   └── style.css
│   ├── templates/         # HTML templates
│   │   └── index.html
│   └── utils/             # Utility functions
│       ├── fasta.py       # FASTA file parsing
│       ├── filesystem.py  # File system operations
│       └── security.py    # Security utilities
├── bin/                   # Algorithm binaries (not in repo)
├── seqs/                  # Sequence datasets (not in repo)
│   ├── Balibase/
│   ├── Benchmark/
│   ├── NUC/
│   └── PROT/
└── results/               # Alignment results (generated)
```

## Requirements

- Python 3.10+
- Flask
- Werkzeug

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/vncsmnl/msa_app
   cd msa_app
   ```

2. **Create a virtual environment** (recommended)
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up directories**
   
   Create the following directories if they don't exist:
   ```bash
   mkdir bin seqs results
   ```

5. **Add algorithm binaries**
   
   Place your A-Star and PA-Star executable binaries in the `bin/` directory.

6.  **Structure**

- `seqs/Benchmark/` - Benchmark test sequences
- `seqs/Balibase/` - BAliBASE benchmark suite
- `seqs/NUC/` - Nucleotide sequences (DNA/RNA)
- `seqs/PAM/` - Protein sequences organized by length


These sequences are used for:
- Testing the MSA algorithms
- Benchmarking performance
- Validating alignment quality

### References

- BAliBASE: [Benchmark Alignment Database](https://lbgi.fr/balibase/)

## Usage

1. **Start the server**
   ```bash
   python app.py
   ```

2. **Access the application**
   
   Open your browser and navigate to:
   ```
   http://localhost:5000
   ```

3. **Run an alignment**
   - Select an algorithm (A-Star or PA-Star)
   - Choose a binary version
   - Browse and select a FASTA sequence file
   - Configure parameters (cost type, thread count)
   - Click "Run" to execute the alignment

4. **View results**
   
   Results are automatically saved and can be viewed through the results interface.

## API Endpoints

### Sequences
- `GET /api/sequences/sources` - List available sequence sources
- `GET /api/sequences/<source>` - Browse sequences in a source
- `GET /api/sequences/<source>/file` - Get sequence file content

### Binaries
- `GET /api/binaries` - List available algorithm binaries

### Execution
- `POST /api/run` - Execute MSA alignment
  - Parameters: algorithm, binary_name, file_path, cost_type, num_threads, verbose

### Results
- `GET /api/results` - List all alignment results
- `GET /api/results/<result_id>` - Get specific result details

## Configuration

Edit `app/config.py` to customize:
- Directory paths
- Sequence sources
- Server settings
- Secret key

## License

MIT License

## Notes

- The application runs with debug mode enabled by default
- Default server port is 5000
- Results are stored locally in the `results/` directory
- Execution timeout is set to 10 minutes per alignment
