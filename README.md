	@DataProvider(name = "OdemePoliceData", parallel = false)
	public Iterator<Object[]> OdemeDegisiklikSelectPolice() throws RemoteException {

		log.info("Total Odeme Police Data Provider: " + odemePoliceList.size());

		Collection<Object[]> data = new ArrayList<Object[]>();
		odemePoliceList.forEach(item -> data.add(new Object[] { item }));
		return data.iterator();
	}

	@Test(dataProvider = "OdemePoliceData")
	public void OdemeDegisikligiTest(String[] dataFromList, Integer i)
			throws InterruptedException, SQLException, As400Exceptions, IOException {

		
		
		String PolicePrefix = dataFromList[0].trim();
		String policeNo = dataFromList[1].trim();
		log.info("Police No: " +PolicePrefix+" "+ policeNo);

		if(!(dataFromList[0].trim().equals("E")|| dataFromList[0].trim().equals("D")))
			throw new As400Exceptions(dataFromList[0], policeNo, "", "Başarısız", "Hata!! Poliçe paket kodu hatalıdır.",
					odemeDegisikligiList);
		if(i==0 || i==1 || i==2 || i==3 || i==4 || i==5) {
			Thread.sleep(i*1000);
		}
			
		try {

			as400Actions.openUrl(GetOdemeDegisikligiData.as400URL, policeNo, odemeDegisikligiList,PolicePrefix)
					.login(GetOdemeDegisikligiData.as400Username, GetOdemeDegisikligiData.as400Password, policeNo, odemeDegisikligiList,PolicePrefix)
					.odemeSekliDegisikligi(policeNo, odemeDegisikligiList,PolicePrefix);

		} catch (Exception e) {

			as400Actions.sessionClose();
			
//			if (e.getMessage().contains("WebDriverException") || e.getMessage().contains("TimeoutException")) {
			if(!e.toString().contains("As400Exceptions")) {
				log.info("exception identification:" + e.getMessage());
				throw new As400Exceptions(PolicePrefix, policeNo, "", "Başarısız", "Odeme Degisikligi Hata: Sistem Exception",
						odemeDegisikligiList);
			}
		}
	}
