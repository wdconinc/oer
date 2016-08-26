namespace :book do
  desc 'prepare build'
  task :prebuild do
    Dir.mkdir 'build' unless Dir.exists? 'build'
    Dir.mkdir 'images' unless Dir.exists? 'images'
    Dir.glob("book/*/images/*").each do |image|
      FileUtils.copy(image, "images/" + File.basename(image))
    end
  end

  desc 'build basic book formats'
  task :build => :prebuild do
    puts "Converting to HTML..."
    `bundle exec asciidoctor -D build oer.asc`
    puts " -- HTML output at build/oer.html"

    puts "Converting to EPub..."
    `bundle exec asciidoctor-epub3 -D build oer.asc`
    puts " -- Epub output at build/oer.epub"

    puts "Converting to Mobi (kf8)..."
    `bundle exec asciidoctor-epub3 -D build -a ebook-format=kf8 oer.asc`
    puts " -- Mobi output at build/oer.mobi"

    puts "Converting to PDF... (this one takes a while)"
    `bundle exec asciidoctor-pdf -D build oer.asc 2>/dev/null`
    puts " -- PDF  output at build/oer.pdf"
  end
end

task :default => "book:build"

