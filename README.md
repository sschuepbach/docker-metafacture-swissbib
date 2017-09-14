# Standalone Metafacture Instance with Swissbib Extensions
## to get an overview of the available metafacture commands
	 docker run dataramblers/metafacture-swissbib:latest
## to start a flux - script (in general) 	 
	docker run  -v /usr/local/swissbib/mfWorkflows/src/main/resources/gh:/mfwf dataramblers/metafacture-swissbib:latest /mfwf/[name].flux


## to start a flux script with access to a mongo storage outside any Mongo Docker container 
    in general not recommended in production because Docker uses Host network
    we use this to access Mongo storage deployed on swissbib hosts
    
    docker run --network host -v /usr/local/swissbib/mfWorkflows/src/main/resources/gh:/mfwf dataramblers/metafacture-swissbib:latest /mfwf/readMongo.flux