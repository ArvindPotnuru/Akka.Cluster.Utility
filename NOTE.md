# DistributedActorDictionary Redesign

 - DistributedActorDictionaryCenter �� Center �� ���� ������ �Ǿ�� �Ѵ�.
   - �̰� �ܺο��� ���̴� �⺻ Actor ���� ��. �̰� �簢�̾���. Node �� implementation detail ����.

 - �ΰ��� use case ��?

   - RoomTable ��
     - �ܺο��� Create ��û�� �ϸ� Dictionary �� �˾Ƽ� round-robin ���� ��򰡿� �ش� actor ��
	   ����� IActorRef �� ��ȯ�Ѵ�. ������ �ش� actor �� ���� ����ϴ� ��� ����
   - UserTable ��
     - Worker Node ���� ���� ���� Dictionary �� ���.
	 - ���Ŀ� RoomTable ó�� ���� ���� �ִ�. (Webby ���� ������ ��?)
	   - �׷��� �̰͵� �ᱹ UserTable �� �� �� �ְڳ�. �׷��ٸ� �� �� API �� Ÿ��Ʈ�ϰ�
	     ���� �� �ֱ� �ϴ�. (���� api �� ��¦ �ٸ���..)

 - API.
   - Dictionary
     - For User
       - Create      : Worker ���� Create ��û �� ���
	   - GetOrCreate : ������ Get. ������ Create
	   - Get
     - For Worker
	   - Created     : ���� ��û�� ���� �Ϸ� �˸�
	   - Removed     : �����ϰ� �ִ� Actor ���� �˸�
   - Worker
     - For User
	   - Add         : ���� Actor �� �����ϰ� ��Ͻ�Ű�� ����
	   - Remove      : Actor �� �Ҹ��� �ƴ� �ɵ������� ������������ �� �� ���
	 - For Dictionary
	   - Create      : ���� ��û

 - ����
   - RoomTable
     - Dict �� Worker �� �ִ�.
	 - Dict �� GetOrCreate ��û�� ������ Worker �� �Բ� ó��
	 - Room �� �Ҹ�Ǹ� Worker �� �޾� Dict ���� �˸�.
   - UserTable
     - User �� ClientGateway �� ���� ������.
	 - ������ User �� Worker or Dict ���� ��� ��û�� ����.
	   - Worker �� �ٽ� 