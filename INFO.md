
# 编译和构建

## 下载和安装

```
wget https://repo.anaconda.com/miniconda/Miniconda3-py39_4.12.0-Linux-x86_64.sh  
sh Miniconda3-py39_4.12.0-Linux-x86_64.sh -b  
~/miniconda3/bin/conda init
. ~/.bashrc
conda create --name d2l python=3.9 -y  # For py3.8: conda create --name d2l python=3.8 -y
conda activate d2l
pip install torch torchvision
pip install d2lbook
git clone https://github.com/d2l-ai/d2l-en.git
git clone https://github.com/d2l-ai/d2l-zh.git
cd d2l-en
pip install -e .  # Install the d2l library from source

```

## 构建不运行程序

Change `eval_notebook = True` to `eval_notebook = False` in `config.ini`.


## 构建pdf PDF

```
# Install d2lbook
pip install git+https://github.com/d2l-ai/d2l-book

sudo apt-get install texlive-full
sudo apt-get install librsvg2-bin
sudo apt-get install pandoc  # If not working, conda install pandoc

# To import d2l
cd d2l-en
pip install -e .

# Build PDF
d2lbook build pdf
```

### 下载英文字体 for PDF

```
wget https://raw.githubusercontent.com/d2l-ai/utils/master/install_fonts.sh
sudo bash install_fonts.sh
```


## 构建 HTML

```
d2lbook build html
```


## 编译PDF版本-中文版本

编译pdf版本需要xelatex、librsvg2-bin（svg图片转pdf）和思源字体。在Ubuntu可以这样安装。

```
sudo apt-get install texlive-full
sudo apt-get install librsvg2-bin
```

```
wget https://github.com/adobe-fonts/source-han-sans/releases/download/2.004R/SourceHanSansSC.zip
wget -O SourceHanSerifSC.zip https://github.com/adobe-fonts/source-han-serif/releases/download/2.001R/09_SourceHanSerifSC.zip

unzip SourceHanSansSC.zip -d SourceHanSansSC
unzip SourceHanSerifSC.zip -d SourceHanSerifSC

sudo mv SourceHanSansSC SourceHanSerifSC /usr/share/fonts/opentype/
sudo fc-cache -f -v


pip install sphinxcontrib-restructuredtext-lexer
pip install sphinx.ext.autosectionlabel
```


## 其他安装

```
python -m spacy download en # 需已 pip install spacy
```

## 样式规范

贡献请遵照本教程的[样式规范](STYLE_GUIDE.md)。

## 中英文术语对照

翻译请参照[中英文术语对照](TERMINOLOGY.md)。
