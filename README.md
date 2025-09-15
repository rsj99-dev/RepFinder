# Archaeal Plasmid Rep Protein Finder / 质粒复制子蛋白基因寻找与注释工具

A comprehensive tool for annotating replication genes in plasmid sequences with support for multiple file formats and batch processing / 支持多种文件格式和批量处理的质粒序列复制子基因寻找与注释工具

## Features / 功能特性

- **Multi-format support / 多格式支持**: FASTA and GenBank files / FASTA和GenBank文件
- **Batch processing / 批量处理**: Process entire directories / 处理整个目录
- **Automatic format detection / 自动格式检测**: No need to specify file type / 无需指定文件类型
- **Flexible alignment / 灵活比对**: DIAMOND or BLAST+ support / 支持DIAMOND或BLAST+
- **Comprehensive output / 全面输出**: JSON, GFF3, and text reports / JSON、GFF3和文本报告

## Dependencies / 依赖

### Python packages / Python包
```bash
pip install biopython
```

### Sequence alignment tool / 序列比对工具
Choose one / 选择其中一个：

**Option 1: DIAMOND (recommended/推荐)**
```bash
conda install -c bioconda diamond
```

**Option 2: BLAST+**
```bash
conda install -c bioconda blast
```

## Installation / 安装

```bash
pip install -e .
```

## Quick Start / 快速开始

### Single File Processing / 单文件处理

```bash
# Process FASTA file / 处理FASTA文件
python -m plasmid_rep_annotator.cli input.fasta

# Process GenBank file / 处理GenBank文件
python -m plasmid_rep_annotator.cli input.gb

# Force use BLAST+ / 强制使用BLAST+
python -m plasmid_rep_annotator.cli input.fasta --aligner blast

# Custom output prefix / 自定义输出前缀
python -m plasmid_rep_annotator.cli input.fasta --output my_results
```

### Batch Processing / 批量处理

```bash
# Process all files in directory / 处理目录中的所有文件
python batch_genbank_annotator.py input_directory

# Specify output directory / 指定输出目录
python batch_genbank_annotator.py input_directory -o output_directory

# Adjust parameters / 调整参数
python batch_genbank_annotator.py input_directory --min-length 50 --identity 20

# Process only specific file types / 只处理特定文件类型
python batch_genbank_annotator.py input_directory --extensions .gb .gbk
```

### Python API

```python
from plasmid_rep_annotator import PlasmidRepAnnotator
from batch_genbank_annotator import BatchGenBankAnnotator

# Single file processing / 单文件处理
annotator = PlasmidRepAnnotator()

# Process FASTA file / 处理FASTA文件
results = annotator.annotate_plasmid_file('input.fasta')

# Process GenBank file / 处理GenBank文件
results = annotator.annotate_plasmid_file('input.gb')

# Batch processing / 批量处理
batch_annotator = BatchGenBankAnnotator()
stats = batch_annotator.process_directory('input_directory', 'output_directory')
```

## Output Files / 输出文件

### Single File Output / 单文件输出
- `*_rep_annotations.json` - JSON format annotations / JSON格式注释
- `*_rep_annotations.gff3` - GFF3 format annotations / GFF3格式注释
- `*_rep_summary.txt` - Text summary / 文本摘要

### Batch Processing Output / 批量处理输出
- Individual files for each input / 每个输入文件的单独输出
- `batch_annotation_report.txt` - Detailed text report / 详细文本报告
- `batch_annotation_summary.json` - JSON summary of all results / 所有结果的JSON汇总

## Parameters / 参数

- `--aligner` - Choose aligner: auto/diamond/blast (default: auto) / 选择比对工具
- `--min-length` - Minimum protein length (default: 100) / 最小蛋白质长度
- `--identity` - Minimum identity threshold (default: 15.0) / 最小同一性阈值
- `--output` - Output prefix / 输出前缀
- `--rep-db` - Custom rep database / 自定义rep数据库

## Examples / 示例

### Single File Examples / 单文件示例

```bash
# Process FASTA file / 处理FASTA文件
python -m plasmid_rep_annotator.cli "质粒fasta/GenBank_U78295.1 Methanosarcina acetivorans plasmid pC2A.fasta"

# Process GenBank file / 处理GenBank文件
python -m plasmid_rep_annotator.cli test_plasmid.gb
```

### Batch Processing Example / 批量处理示例

```bash
# Process all plasmid files in directory / 处理目录中的所有质粒文件
python batch_genbank_annotator.py "质粒fasta" -o results
```

This will process all FASTA and GenBank files in the directory and generate comprehensive reports / 这将处理目录中的所有FASTA和GenBank文件并生成全面的报告。
