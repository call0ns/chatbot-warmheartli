scrapy:
sudo pip install scrapy
scrapy crawl --logfile=subtitle.log subtitle &

cd result
i=0; for file in `ls | grep -E ".zip|.rar"`; do mkdir -p output/${i}; unar "$file" -o output/${i} >> output/output.log; ((i++)); done
find output/ -name "*.srt" -or -name "*.ass" -or -name "*.ssa" | wc -l

mkdir -p input/srt
find output/ -name "*.srt" -exec mv "{}" ./input/srt \;
mkdir -p input/ass
find output/ -name "*.ass" -exec mv "{}" ./input/ass \;
mkdir -p input/ssa
find output/ -name "*.ssa" -exec mv "{}" ./input/ssa \;

