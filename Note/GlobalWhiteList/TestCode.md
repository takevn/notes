# Mock getModel function
HashMap<Long, RequestDomainModel> domainModelMap = new HashMap<>();
RequestDomainModel requestDomainModel1 = new RequestDomainModel(1L,"reemo.me", "www.reemo.me",time, time);
RequestDomainModel requestDomainModel2 = new RequestDomainModel(2L,"gmoam.jp", "www.gmoam.jp",time, time);
RequestDomainModel requestDomainModel3 = new RequestDomainModel(3L,"gmo.shop", "www.gmo.shop",time, time);
domainModelMap.put(1l, requestDomainModel1);
domainModelMap.put(2l, requestDomainModel2);
domainModelMap.put(3l, requestDomainModel3);


new MockUp<RequestDomainModel>() {
    @Mock
    public RequestDomainModel getModel(Long domainId) {
        return domainModelMap.get(domainId);
    }
};
