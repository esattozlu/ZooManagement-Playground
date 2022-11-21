# ZooManagement Playground

- ZooManagementApp.playgorund, Hayvanat bahçesi yönetimi için oluşturulmuş bir playground dosyasıdır.

- Hayvanat bahçesi, isim, su limiti ve bütçe ile oluşturulabilir. Daha sonra getNewAnimal ve hireZooKeeper methodlarıyla yeni hayvan ve bakıcı eklenebilir.

- getNewAnimal methodu sadece yeni hayvan oluşturulurken kullanılır. Eğer mevcut hayvan sayısını arttırmak istiyorsak getNewAnimal methodu daha önce bu hayvanın oluşturulduğuna dair uyarı verecektir. Bu durumda addToExisting methodu ile ekleme yapılmalıdır.

- Yeni hayvan eklerken de, mevcuta ekleme yaparken de su limiti, hayvanların tüketimlerinden fazla olmalıdır. Eğer değilse su limitinin en az ne kadar arttırılması gerektiği uyarısı alınır. Bu durumda increaseWaterLimit ile istenen miktarda artış yapılabilir veya reviseWaterLimit ile toplam water limit değiştirilebilir.

- Bakıcı sayısı arttırılmak istenirse hireZooKeeper methodu kullanılabilir. Bakıcı eklerken id'nin mevcut bakıcı id'lerinden farklı olması gerekmektedir. Eğer aynı id'li çalışan eklenmeye çalışılırsa uyarı alınacaktır ve çalışan oluşturulamayacaktır.

- addIncome methoduyla bütçeye gelir, addExpense methoduyla gider oluşturulabilir. Eğer gider bütçeden yüksek ise expense girişi yapılamaz ve uyarı alınır.

- Çalışan maaşları baktıkları hayvan türü sayısına göre hayvan başına 0,05 prim katsayısı ile hesaplanır. Baz maaş 7000₺'dir.
- paySalary methodu ile çalışan maaşları ödenebilir. Completion'ında ZooKeeper array döner. Bu array'den maaşlar ödendikten sonra kime ne kadar maaş ödenmiş, kaç hayvandan sorumlu gibi bilgiler öğrenilebilir.
- Eğer maaş ödemesi için yeterli bütçe yoksa ödeme yapılamaz ve uyarı alınır.

- Kalan su limiti askRemainingWaterLimit methoduyla sorgulanabilir.

### SUCCESS MESSAGES:

- Hayvanat bahçesi oluştuğunda: "\(zooName) Zoo is created with \(waterLimit) water limit, \(budget)₺ budget."
- waterLimit değiştirildiğinde: "Water limit is changed to \(waterLimit)"
- waterLimit arttırıldığında: "Water limit is increased by \(amount) to \(waterLimit)"
- Gelir eklendiğinde: "Income is added. Previos budget: \(previousBudget)₺, new budget: \(budget)₺"
- Gider eklendiğinde: "Expense is added. Previos budget: \(previousBudget)₺, new budget: \(budget)₺"
- Maaşlar ödendiğinde: "\(totalSalary)₺ keeper salaries are paid. Remaining budget: \(budget)₺."
- Yeni hayvan eklendiğinde: "\(animal.animalType) type, \(animalBreed) breed animal is added."
- Bakıcı işe alındığında: "Keeper \(keeper.name) is hired."
- Kalan su limiti sorgulandığında: "Remaining water limit:", remainingLimit
- Mevcut hayvana ekleme yapıldığında: "\(previousCount) \(animal.animalBreed) increased to \(animals[index].count)."

### FAILURE MESSAGES:

- Hayvan array'i ile hayvanat bahçesi oluşturulurken eğer hayvanların su tüketimi limitin üzerindeyse: "Total consumption(\(totalConsumption)) of animals is higher than Water Limit. Please increase Water Limit at least \(totalConsumption - waterLimit)"
- Bütçede yeterli tutar yokken expense girilmek istendiğinde: "There is not enough money to pay expense. Please add income to budget case."
- Çalışan maaşları ödenmek istendiğinde yeterli bütçe yoksa: "There is not enough money to pay salaries. Please add income to budget case."
- Çalışan yokken çalışan maaşı ödenmek istendiğinde: "There is no keeper to pay salary."
- Yeni hayvan eklenirken su limiti yetmezse: "Remaining water limit of zoo is not enough to get \(count) \(animalBreed). Please increase the water limit at least \(animal.waterConsumption * Double(animal.count) - remainingLimit)."
- Yeni eklenmek istenen hayvan daha önce oluşturulmuşsa: "There is already an animal with type: \(animalType), breed: \(animalBreed). Please call addToExisting function."
- Bakıcı eklenirken aynı id'ye sahip bakıcı eklenirse: "There is already a keeper with id: \(keeper.keeperId). Please try another id."
- Hayvan eklenmemişken mevcut hayvana yeni ekleme yapılmak istendiğinde: "There is no animal in the zoo. Please use getNewAnimal method."
- Mevcut hayvana ekleme yapılmak istendiğinde su limiti yeterli değilse: "There is not enough water limit to add \(count) \(animalType) typed \(animalBreed). Please increase the water limit at least \(animal.waterConsumption * Double(count) - remainingLimit)"
- Mevcut hayvana ekleme yapılmak istendiğinde daha önce tanımlanmayan giriş yapıldığında: "Type: \(animalType), breed: \(animalBreed) animal is not previosly defined. Please use getNewAnimal method."
