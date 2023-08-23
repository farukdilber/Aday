	private  void kontrolEndeks(List<String[]> tarihBilgisi) {
		try {
		//	if(isElementExist(By.id("inpR6C3L1.id"), 2));
			as400SendKeysEnter(By.id("inpR7C2L1.id"), "X");
			sendKeysWithLabel("Pol/Söz.Bilgilerini Görüntüleme ..:", "X");
			as400PressEnter();
			as400PressEnter();
			as400PressEnter();
			as400PressEnter();
			
			String Gun = getTextOfElement(By.xpath("//*[@id=\"screenarea\"]/tbody/tr[5]/td[10]/a"), 0);
			String Ay = getTextOfElement(By.xpath("//*[@id=\"screenarea\"]/tbody/tr[5]/td[12]/a"), 0);
			String Yıl = getTextOfElement(By.xpath("//*[@id=\"screenarea\"]/tbody/tr[5]/td[14]/a"), 0);
			log.info(Gun + " " + Ay + " " + Yıl);
			String[] temp = new String[1];
			String[] temp1 = new String[1];
			String[] temp2 = new String[1];
			temp[0] = Gun;
			temp1[0] = Ay;
			temp2[0] = Yıl;
			tarihBilgisi.add(temp);
			tarihBilgisi.add(temp1);
			tarihBilgisi.add(temp2);

			System.out.println(temp + " " + temp1 +" "+ temp2);
			
				
		} catch (InterruptedException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
	}
