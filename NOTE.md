# DistributedActorTable Shutdown?

 - Cluster �� down �Ǿ��ų� down �� ��ó�� ���� �� Container �� ��� �ؾ� �ϳ�?
   - Container �� down �Ǹ� �ش� container �� actor �� ���� ������ �����Ѵ�.
   - down �� �� ó�� ���δٸ� cluster �� �̹� actor �� ���� ó������ ���̹Ƿ� �� ��쿡��
     ��� �ִ� actor �� ��� ���� �ϴ� ���� �Ǵ�.
   - ���� container �� down �� ���̶�� ��� �ϳ�?
     �̷������� container �� ���Ӱ� ������ ���̶�� ��� �ִ� actor �� �Ѱ��� �� �ִ�.
     �ٸ� �� ��� �ٸ� container �� race condition �� �߻��� �� �����Ƿ� conflict ó���� ����� �Ѵ�.

# DistributedActorTable Rework (DONE)

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