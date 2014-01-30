require 'fileutils'
def generator_for_post
# Dir["/home/cvapp/task/**/*.html"]  # used for recursively finding all the files present in a 
b=[]
i=1
task_path=Dir.pwd
posts_path=task_path+'/posts/'
Dir.foreach(posts_path) do |item|
   next if item == '.' or item == '..' 
   puts item
   k,v=item.split('.')
   k1=k.split('-')
   for j in 0..3 
   x="" 
   y=""
   if j<=2
         b[j]=k1[j]
   else 
        size=3
       while size < (k1.size)
        x = x+"-"+k1[size]
         size = size+1 
       end
       b[j]=x
       #puts b  
    for i in (0..b.size-1)
      y=y+'/'+b[i]  
    end
       generated_path=task_path+'/site'+y
       FileUtils.mkpath generated_path
       index_path=generated_path+'/index.html' 
       fread=posts_path+item
       File.open(index_path,'w') { |f| f.write(File.read(fread))} 
   end
   end #end of for
end
end #end of generator_for_post
generator_for_post   #method calling
puts "--------------------"
def generator_pages
task_path=Dir.pwd
pages_path=task_path+'/pages/'
           Dir.foreach(pages_path) do |item|
                    next if item == '.' or item == '..' 
                    k,v=item.split('.')
             pages_gpath=task_path+'/site/'+k
             index_path=pages_gpath+'/index.html'
           FileUtils.mkpath pages_gpath
             fread=pages_path+item
           File.open(index_path,'w') { |f| f.write(File.read(fread))}                   
          end  #end of do  
end #end of generator_pages  
  
generator_pages 













