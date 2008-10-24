;; source files
(set @m_files     (filelist "^objc/.*.m$"))
(@m_files unionSet:(filelist "^unzip101e-src/.*\.c$"))

(set @nu_files 	  (filelist "^nu/.*nu$"))

(set SYSTEM ((NSString stringWithShellCommand:"uname") chomp))
(case SYSTEM
      ("Darwin"
               (set @cflags "-g -DDARWIN -I unzip101e-src -std=gnu99")
               (set @ldflags  "-framework Foundation -framework Nu -lz"))
      (else nil))

;; framework description
(set @framework "NuZip")
(set @framework_identifier "nu.programming.nuzip")
(set @framework_creator_code "????")

(compilation-tasks)
(framework-tasks)

(task "clobber" => "clean" is
      (SH "rm -rf tmp nuzip_test nuzip_test.zip")
      (SH "rm -rf #{@framework_dir}"))

(task "default" => "framework")

(task "doc" is (SH "nudoc"))

(task "install" => "framework" is
      (SH "sudo cp nunjad /usr/local/bin")
      (SH "sudo rm -rf /Library/Frameworks/#{@framework}.framework")
      (SH "ditto #{@framework}.framework /Library/Frameworks/#{@framework}.framework"))

(task "test" => "framework" is
      (SH "nutest test/test_*.nu"))
