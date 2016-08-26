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
    `bundle exec pandoc book/*.md book/*/*.md -t html -o build/oer.html`
    puts " -- HTML output at build/oer.html"

    puts "Converting to EPub..."
    `bundle exec pandoc book/*.md book/*/*.md -t epub3 -o build/oer.epub`
    puts " -- Epub output at build/oer.epub"

    puts "Converting to PDF... (this one takes a while)"
    `bundle exec pandoc book/*.md book/*/*.md --latex-engine=xelatex -t latex -o build/oer.pdf`
    puts " -- PDF  output at build/oer.pdf"
  end
end

task :default => "book:build"

