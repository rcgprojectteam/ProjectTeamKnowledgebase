Log into the Clients Tenant
	Click "Show All" in the left panel to expand the options
	Under the header "Admin centers" on the left panel click on "Security" (a new window will open)
		On the left panel click "Policies & Rules"
		In the main window click "Threat Policies"
			Under the "Rules" header click "Email authentication settings"
				Under the main window header "Email authentication settings" there will be two tabs "ARC" and "DKIM" click on "DKIM"
					The DomainKeys Identified Mail (DKIM) will now be displayed
						Click on the required Domains and a new panel will show up on the right side of the window
							Click "Create DKIM keys"
							A new window will pop up with the client's tenant information that will need to be added to their DNS record. 
								The DNS Record should look like this, THIS IS A <CNAME> RECORD.
									Host name: selector1._domainkey
									Points to address or value:    selector1-<DOMAIN>-<SUFFIX>._domainkey.<DOMAIN>.onmicrosoft.com
									TTL: 3600
										AND
									Host name: selector2._domainkey
									Points to address or value:    selector2-<DOMAIN>-<SUFFIX>._domainkey.<DOMAIN>.onmicrosoft.com
									TTL: 3600

![[DKIM Setup Tenant.gif]]