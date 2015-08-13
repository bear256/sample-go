## Parse ini configuration file

Packages:
* github.com/miguel-branco/goconfig

>
	func readIni() {
		c, err := goconfig.ReadConfigFile("config.cfg")
		if err != nil {
			log.Fatalln(err)
		}
		// result is string :http://www.example.com/some/path"
		url, _ := c.GetString("service-1", "url")
		maxclients, _ := c.GetInt64("service-1", "maxclients") // result is int 200
		delegation, _ := c.GetBool("service-1", "delegation")  // result is bool true
	
		// result is string "This is a multi-line\nentry"
		comments, _ := c.GetString("service-1", "comments")
		fmt.Println(url, maxclients, delegation, comments)
	}
	
	func writeIni() {
		c := goconfig.NewConfigFile()
		c.AddSection("section")
		c.AddOption("section", "option", "value")
		// use 0644 as file permission
		c.WriteConfigFile("config.ini", 0644, "A header for this file")
	}