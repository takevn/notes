@Override
protected void addCache(CommonWhiteDomainReviewModel model) {
    Long requestDomainId = model.getCommonWhiteDomainId();
    String domain = CommonWhiteDomainModel.getModel(requestDomainId).getDomain();
    String reversed = new StringBuilder(domain).reverse().toString();

    domainCacheMap.get(model.getSspId()).add(reversed);
}
->

@Override
protected void addCache(CommonWhiteDomainReviewModel model) {
    Optional<String> optional = Optional.ofNullable(model.getCommonWhiteDomainModel())
            .map(CommonWhiteDomainModel::getDomain);
    if (optional.isPresent()) {
        String reversed = new StringBuilder(optional.get()).reverse().toString();
        domainCacheMap.get(model.getSspId()).add(reversed);
    }
}
